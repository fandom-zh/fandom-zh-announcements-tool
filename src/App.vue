<template>
  <AppBar />
  <section id="announcements">
    <h2 id="output">Annoucements</h2>
    <div class="form">
      <FormWrapper title="Input (Discord Format)" form-id="input">
        <div>
          <label for="type">Type of Announcement</label>
          <select v-model="type" name="type" id="type">
            <option value="news">Annoucement / 公告</option>
            <option value="help">Help / 帮助 / 說明</option>
            <option value="breaking">Breaking News / 重大公告</option>
          </select>
        </div>
        <div>
          <label for="url">URL</label>
          <input v-model="url" type="url" name="url" id="url">
        </div>
        <div>
          <label for="date">Date</label>
          <input v-model="date" type="date" name="date" id="date">
        </div>
        <div>
          <label for="everyone">@everyone</label>
          <input v-model="everyone" type="checkbox" name="everyone" id="everyone">
        </div>
        <br>
        <div>
          <label for="zh-tw">zh-Hant-TW</label>
          <textarea
            v-model="zhTW"
            id="zh-tw"
            name="zh-tw"
            spellcheck
            rows="20"
            title="Please put zh-TW message here. You can convert zh-CN to zh-TW using the conversion tool below (WIP). Supports **, * and ` decorator."
            placeholder="Please put zh-TW message here. You can convert zh-CN to zh-TW using the conversion tool below (WIP). Supports **, * and ` decorator."
          ></textarea>
        </div>
        <div>
          <label for="zh-cn">zh-Hans-CN</label>
          <textarea
            v-model="zhCN"
            id="zh-cn"
            name="zh-cn"
            spellcheck
            rows="20"
            title="Please put zh-CN message here. You can convert zh-TW to zh-CN using the conversion tool below (WIP). Supports **, * and ` decorator."
            placeholder="Please put zh-CN message here. You can convert zh-TW to zh-CN using the conversion tool below (WIP). Supports **, * and ` decorator."
          ></textarea>
        </div>
      </FormWrapper>
      <FormWrapper title="Output">
        <div>
          <label for="discord">Discord</label>
          <textarea
            v-model="discord"
            id="discord"
            name="discord"
            spellcheck
            rows="20"
            title="Output for Discord."
            placeholder="Output for Discord."
            readonly
          ></textarea>
        </div>
        <div>
          <label for="telegram">Telegram</label>
          <textarea
            v-model="telegram"
            id="telegram"
            name="telegram"
            spellcheck
            rows="20"
            title="Output for Telegram."
            placeholder="Output for Telegram."
            readonly
          ></textarea>
        </div>
        <div>
          <label for="line">LINE</label>
          <textarea
            v-model="line"
            id="line"
            name="line"
            spellcheck
            rows="20"
            title="Output for LINE."
            placeholder="Output for LINE."
            readonly
          ></textarea>
        </div>
        <div>
          <label for="qq">QQ</label>
          <textarea
            v-model="qq"
            id="qq"
            name="qq"
            spellcheck
            rows="20"
            title="Output for QQ."
            placeholder="Output for QQ."
            readonly
          ></textarea>
        </div>
        <div>
          <label for="lqa">LQA</label>
          <textarea
            v-model="lqa"
            id="lqa"
            name="lqa"
            spellcheck
            rows="20"
            title="Output for LQA."
            placeholder="Output for LQA."
            readonly
          ></textarea>
        </div>
      </FormWrapper>
    </div>
  </section>
  <section>
    <h2>Language Conversion</h2>
    <div id="lc">
      <FormWrapper title="WIP">
        A work in progress.
      </FormWrapper>
    </div>
  </section>
  
</template>

<script setup>
import FormWrapper from './components/FormWrapper.vue'
import AppBar from './components/AppBar.vue'
import { watch } from 'vue'

ref: type = ''
ref: url = ''
ref: date = ''
ref: zhTW = ''
ref: zhCN = ''
ref: discord = ''
ref: telegram = ''
ref: line = ''
ref: qq = ''
ref: lqa = ''
ref: everyone = ''

const updateOutput = async () => {
  let msgDC = []
  let msgLN = []
  let msgTG = []
  let msgQQ = []

  if (everyone) {
    msgDC.push('@everyone \n')
  }
  // Date
  const dayTable = {
    0: 'Sun',
    1: 'Mon',
    2: 'Tue',
    3: 'Wed',
    4: 'Thu',
    5: 'Fri',
    6: 'Sat'
  }
  if (date) {
    let time = new Date(date)
    let timeParsed = date.replace(/-/g, '/') + ' ' + dayTable[time.getDay()] + '.'
    msgDC.push(timeParsed)
    msgLN.push(timeParsed)
    msgTG.push(timeParsed)
    msgQQ.push(timeParsed)
  }

  // Type Prefix
  const typeTable = {
    news: {
      zhTW: '公告',
      zhCN: '公告'
    },
    help: {
      zhTW: '説明',
      zhCN: '帮助'
    },
    breaking: {
      zhTW: '重大公告',
      zhCN: '重大公告'
    },
  }

  if (zhTW) {
    if (type) {
      msgDC.push(`**[ ${typeTable[type].zhTW} ]**`)
      msgLN.push(`[ ${typeTable[type].zhTW} ]`)
      msgTG.push(`**[ ${typeTable[type].zhTW} ]**`)
    }
    let zhTWPlaintext = zhTW.replace(/((?<!\\)\*)*/g, '').replace(/((?<!\\)`*){1}/g, '').replace(/\\(?=(`|\\|\*))/g, '')
    let zhTWTG = zhTW.replace(/(?<!\\)(?<!\*)\*(?!\*)/g, '__')

    msgDC.push(zhTW)
    msgLN.push(zhTWPlaintext)
    msgTG.push(zhTWTG)
    if (zhCN) {
      msgDC.push('\n----\n')
      msgLN.push('\n----\n')
      msgTG.push('\n----\n')
    }
  }

  if (zhCN) {
    if (type) {
      msgDC.push(`**[ ${typeTable[type].zhCN} ]**`)
      msgLN.push(`[ ${typeTable[type].zhCN} ]`)
      msgTG.push(`**[ ${typeTable[type].zhCN} ]**`)
    }
    let zhCNPlaintext = zhCN.replace(/((?<!\\)\*)*/g, '').replace(/((?<!\\)`*){1}/g, '').replace(/\\(?=(`|\\|\*))/g, '')
    let zhCNTG = zhCN.replace(/(?<!\\)(?<!\*)\*(?!\*)/g, '__')

    msgDC.push(zhCN)
    msgLN.push(zhCNPlaintext)
    msgQQ.push(zhCNPlaintext)
    msgTG.push(zhCNTG)
  }

  if (url) {
    let urlEncoded = encodeURI(url)
    let urlDecoded = decodeURI(url)
    msgDC.push('\n' + urlDecoded)
    msgLN.push('\n' + urlDecoded)
    msgQQ.push('\n' + urlEncoded)
    msgTG.push('\n' + urlDecoded)
  }

  // Apply it
  discord = msgDC.join('\n')
  telegram = msgTG.join('\n')
  line = msgLN.join('\n')
  qq = msgQQ.join('\n')
  lqa = 'Discord\n```md\n' + discord + '\n```\nTelegram\n```md\n' + telegram + '```\nLINE\n```\n' + line + '```\nQQ\n```\n' + qq + '\n```'
}

watch([$everyone, $type, $url, $date, $zhTW, $zhCN], updateOutput)
</script>

<style>
#app {
  font-family: 'Rubik', Helvetica, Arial, sans-serif;
  margin-top: 65px;
}
h2 {
  margin-left: 15px;
  display: inline-block;
  background-image: linear-gradient(to top,rgba(0,155,190,0.15) 54%,transparent 54%,transparent 100%);
}
body {
  margin: 0;
}
legend {
  padding-left: 5px;
  padding-right: 5px;
}
textarea {
  resize: none;
}
label {
  display: block;
}
fieldset > div {
  display: inline-block;
  margin: 5px;
}
</style>
