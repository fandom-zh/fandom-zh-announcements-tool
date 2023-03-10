<template>
  <AppBar />
  <section id="announcements">
    <h2 id="output">Announcements</h2>
    <div class="form">
      <FormWrapper title="Input (Discord Format)" form-id="input">
        <div>
          <label for="type">Type of Announcement</label>
          <select v-model="type" name="type" id="type">
            <option value="news">Announcement / 公告</option>
            <option value="help">Help / 帮助 / 說明</option>
            <option value="breaking">Breaking News / 重大公告</option>
          </select>
        </div>
        <div>
          <label for="url">URL</label>
          <input v-model="url" type="url" name="url" id="url" />
        </div>
        <div>
          <label for="date">Date</label>
          <input v-model="date" type="date" name="date" id="date" />
        </div>
        <div>
          <label for="everyone">@everyone</label>
          <input
            v-model="everyone"
            type="checkbox"
            name="everyone"
            id="everyone"
          />
        </div>
        <br />
        <div>
          <label for="zh-tw">zh-Hant-TW</label>
          <textarea
            v-model="zhTW"
            id="zh-tw"
            name="zh-tw"
            spellcheck
            rows="20"
            title="Please put zh-Hant-TW message here. You can convert zh-Hans-CN to zh-Hant-TW using the conversion tool below. Supports **, * and ` decorator."
            placeholder="Please put zh-Hant-TW message here. You can convert zh-Hans-CN to zh-Hant-TW using the conversion tool below. Supports **, * and ` decorator."
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
            title="Please put zh-Hans-CN message here. You can convert zh-Hant-TW to zh-Hans-CN using the conversion tool below. Supports **, * and ` decorator."
            placeholder="Please put zh-Hans-CN message here. You can convert zh-Hant-TW to zh-Hans-CN using the conversion tool below. Supports **, * and ` decorator."
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
          <label for="line">Line</label>
          <textarea
            v-model="line"
            id="line"
            name="line"
            spellcheck
            rows="20"
            title="Output for Line."
            placeholder="Output for Line."
            readonly
          ></textarea>
        </div>
        <div>
          <label for="bahamut">Bahamut</label>
          <textarea
            v-model="bahamut"
            id="bahamut"
            name="bahamut"
            spellcheck
            rows="20"
            title="Output for Bahamut."
            placeholder="Output for Bahamut."
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
      <FormWrapper title="Input">
        <div>
          <label for="target">Target Variant</label>
          <select v-model="target" name="target" id="target">
            <option value="zh-TW">zh-Hant-TW / 臺灣正體</option>
            <option value="zh-HK">zh-Hant-HK / 香港繁體</option>
            <option value="zh-MO">zh-Hant-MO / 澳門繁體</option>
            <option value="zh-CN">zh-Hans-CN / 大陆简体</option>
            <option value="zh-MY">zh-Hans-MY / 大马简体</option>
            <option value="zh-SG">zh-Hans-SG / 新加坡简体</option>
          </select>
        </div>
        <div>
          <label for="cgroup">NoteTA CGroup</label>
          <input
            v-model="cgroup"
            type="cgroup"
            name="cgroup"
            id="cgroup"
            title="Use comma to separate multiple CGroups."
            placeholder="Use comma to separate multiple CGroups."
          />
        </div>
        <div>
          <label for="wikiUrl">api.php</label>
          <input
            v-model="wikiUrl"
            type="wikiUrl"
            name="wikiUrl"
            id="wikiUrl"
          />
        </div>
        <br />
        <div>
          <label for="content">Content</label>
          <textarea
            v-model="content"
            id="zh-cn"
            name="zh-cn"
            spellcheck
            rows="20"
            title="Please put the message you want to convert here. Support MediaWiki -{}- conversion settings."
            placeholder="Please put the message you want to convert here. Support MediaWiki -{}- conversion settings."
          ></textarea>
        </div>
        <div>
          <button @click="convert()">Submit</button>
        </div>
      </FormWrapper>
      <FormWrapper title="Output">
        <div>
          <label for="output">Output</label>
          <textarea
            v-model="output"
            id="output"
            name="output"
            spellcheck
            rows="20"
            title="Conversion Output here."
            placeholder="Conversion Output here."
            readonly
          ></textarea>
        </div>
      </FormWrapper>
    </div>
  </section>
  <footer>
    <div>
      <div id="disclaimer">
        Powered by Fandom ZH Team. Not an official Fandom product. Not operated
        by or affiliated with Fandom, Inc.
      </div>
      <div id="github">
        <a href="https://github.com/fandom-zh/fandom-zh-announcements-tool"
          >GitHub</a
        >
      </div>
    </div>
  </footer>
</template>

<script setup>
import FormWrapper from "./components/FormWrapper.vue";
import AppBar from "./components/TheAppBar.vue";
import { ref, watch } from "vue";

ref: type = "news";
ref: url = "";
ref: date = "";
ref: zhTW = "";
ref: zhCN = "";
ref: discord = "";
ref: telegram = "";
ref: line = "";
ref: bahamut = "";
ref: qq = "";
ref: lqa = "";
ref: everyone = "";

const updateOutput = async () => {
  let msgBH = [];
  let msgDC = [];
  let msgLN = [];
  let msgTG = [];
  let msgQQ = [];

  let urlConverted = url.replace(
    /(用户博客|%E7%94%A8%E6%88%B7%E5%8D%9A%E5%AE%A2):/g,
    "User_blog:"
  );
  let urlEncoded = encodeURI(decodeURI(urlConverted)); // Intended script design
  let urlDecoded = decodeURI(urlConverted);

  if (everyone) {
    msgDC.push("@everyone \n");
  }
  // Date
  const dayTable = {
    0: "Sun",
    1: "Mon",
    2: "Tue",
    3: "Wed",
    4: "Thu",
    5: "Fri",
    6: "Sat",
  };
  if (date) {
    let time = new Date(date);
    let timeParsed =
      date.replace(/-/g, "/") + " " + dayTable[time.getDay()] + ".";
    msgBH.push(timeParsed);
    msgDC.push(timeParsed);
    msgLN.push(timeParsed);
    msgTG.push(timeParsed);
    msgQQ.push(timeParsed);
  }

  // Type Prefix
  const typeTable = {
    news: {
      zhTW: "公告",
      zhCN: "公告",
    },
    help: {
      zhTW: "説明",
      zhCN: "帮助",
    },
    breaking: {
      zhTW: "重大公告",
      zhCN: "重大公告",
    },
  };

  if ((zhTW || zhCN) && (type === "news" || type === "breaking")) {
    msgTG.push("#fandom公告\n");
  }

  if (zhTW) {
    msgDC.push("*[ zh-Hant-TW ]*");
    msgTG.push("__[ zh-Hant-TW ]__");
    if (type) {
      msgDC.push(`**[ ${typeTable[type].zhTW} ]**`);
      msgBH.push(`[ ${typeTable[type].zhTW} ]`);
      msgLN.push(`[ ${typeTable[type].zhTW} ]`);
      msgTG.push(`**[ ${typeTable[type].zhTW} ]**`);
    }
    let zhTWParsed = await parse(zhTW);

    msgBH.push(zhTWParsed.msgBH);
    msgDC.push(zhTWParsed.msgDC);
    msgLN.push(zhTWParsed.msgLN);
    msgTG.push(zhTWParsed.msgTG);

    if (zhCN) {
      msgDC.push("\n----\n");
      msgLN.push("\n----\n");
      msgTG.push("\n----\n");
    }
  }

  if (zhCN) {
    msgDC.push("*[ zh-Hans-CN ]*");
    msgTG.push("__[ zh-Hans-CN ]__");
    if (type) {
      msgDC.push(`**[ ${typeTable[type].zhCN} ]**`);
      msgTG.push(`**[ ${typeTable[type].zhCN} ]**`);
    }
    let zhCNParsed = await parse(zhCN);

    msgDC.push(zhCNParsed.msgDC);
    msgQQ.push(zhCNParsed.msgQQ);
    msgTG.push(zhCNParsed.msgTG);
  }

  if ((zhTW || zhCN) && url) {
    msgDC.push("\n" + urlDecoded);
    msgLN.push("\n" + urlDecoded);
    msgTG.push("\n" + urlDecoded);
  }
  if (zhCN && url) {
    msgQQ.push("\n" + urlEncoded);
  }

  // Apply it
  discord = msgDC.join("\n");
  telegram = msgTG.join("\n");
  bahamut = msgBH.join("\n");
  line = msgLN.join("\n");
  qq = msgQQ.join("\n");
  if (everyone || type || url || date || zhTW || zhCN) {
    lqa =
      "Discord\n```md\n" +
      discord +
      "\n```\nTelegram\n```md\n" +
      telegram +
      "```\nBahamut\n```\n" +
      bahamut +
      "```\nLine\n```\n" +
      line +
      "```\nQQ\n```\n" +
      qq +
      "\n```";
  } else {
    lqa = "";
  }

  async function parse(input) {
    const tagDC = /(?<!\\)<dc>((.)*?)<\/dc>/g;
    const tagQQ = /(?<!\\)<qq>((.)*?)<\/qq>/g;
    const tagBH = /(?<!\\)<bh>((.)*?)<\/bh>/g;
    const tagLN = /(?<!\\)<ln>((.)*?)<\/ln>/g;
    const tagTG = /(?<!\\)<tg>((.)*?)<\/tg>/g;

    const noDC = /(?<!\\)<no-dc>((.)*?)<\/no-dc>/g;
    const noQQ = /(?<!\\)<no-qq>((.)*?)<\/no-qq>/g;
    const noBH = /(?<!\\)<no-bh>((.)*?)<\/no-bh>/g;
    const noLN = /(?<!\\)<no-ln>((.)*?)<\/no-ln>/g;
    const noTG = /(?<!\\)<no-tg>((.)*?)<\/no-tg>/g;

    let msgDC = input
      .replace(tagDC, "$1")
      .replace(tagQQ, "")
      .replace(tagBH, "")
      .replace(tagLN, "")
      .replace(tagTG, "")
      .replace(noDC, "")
      .replace(noQQ, "$1")
      .replace(noBH, "$1")
      .replace(noLN, "$1")
      .replace(noTG, "$1");
    let msgQQ = input
      .replace(tagDC, "")
      .replace(tagBH, "")
      .replace(tagLN, "")
      .replace(tagTG, "")
      .replace(noDC, "$1")
      .replace(noQQ, "")
      .replace(noBH, "$1")
      .replace(noLN, "$1")
      .replace(noTG, "$1")
      .replace(/((?<!\\)\*)*/g, "")
      .replace(/((?<!\\)`*){1}/g, "")
      .replace(/\\(?=(`|\\|\*))/g, "");
    let msgBH = input
      .replace(tagDC, "")
      .replace(tagQQ, "")
      .replace(tagLN, "")
      .replace(tagTG, "")
      .replace(noDC, "$1")
      .replace(noQQ, "$1")
      .replace(noBH, "")
      .replace(noLN, "$1")
      .replace(noTG, "$1");
    let msgLN = input
      .replace(tagDC, "")
      .replace(tagQQ, "")
      .replace(tagBH, "")
      .replace(tagTG, "")
      .replace(noDC, "$1")
      .replace(noQQ, "$1")
      .replace(noBH, "$1")
      .replace(noLN, "")
      .replace(noTG, "$1");
    let msgTG = input
      .replace(tagQQ, "")
      .replace(tagBH, "")
      .replace(tagLN, "")
      .replace(tagDC, "")
      .replace(noDC, "$1")
      .replace(noQQ, "$1")
      .replace(noBH, "$1")
      .replace(noLN, "$1")
      .replace(noTG, "")
      .replace(/(?<!\\)(?<!\*)\*(?!\*)/g, "__");

    return {
      msgDC: msgDC,
      msgQQ: msgQQ,
      msgBH: msgBH,
      msgLN: msgLN,
      msgTG: msgTG,
    };
  }
};

watch([$everyone, $type, $url, $date, $zhTW, $zhCN], updateOutput);

ref: content = "";
ref: target = "";
ref: output = "";
ref: cgroup = "";
ref: wikiUrl = "https://community.fandom.com/zh/api.php"

const convert = async () => {
  let noteTACfg;
  if (cgroup) {
    let groups = cgroup.split(",");
    let n = 1;
    let noteTA = [];
    for (let g of groups) {
      noteTA[n-1] = (`G${n}=${g}`);
      n++;
    }
    noteTACfg = '|' + noteTA.join("|");
  }
  const param = new URLSearchParams();
  param.append("action", "parse");
  param.append(
    "text",
    "{{NoteTA"+ noteTACfg +"}}FANDOM_ZH_ANNOUNCEMENTS_TOOL_START__" +
      content.replace(/\n/g, "FANDOM_ZH_ANNOUNCEMENTS_TOOL_BREAK") +
      "__FANDOM_ZH_ANNOUNCEMENTS_TOOL_END"
  );
  param.append("variant", target);
  param.append("format", "json");
  param.append("contentmodel", "wikitext");
  param.append("origin", "*");
  fetch(wikiUrl + "?" + param.toString())
    .then(async (req) => {
      let result = await req.json();
      let out = result.parse.text["*"];
      const ele = document.createElement("textarea");
      ele.innerHTML = out
        .replace(/(.)*FANDOM_ZH_ANNOUNCEMENTS_TOOL_START__/s, "")
        .replace(/__FANDOM_ZH_ANNOUNCEMENTS_TOOL_END(.)*/s, "")
        .replace(/FANDOM_ZH_ANNOUNCEMENTS_TOOL_BREAK/g, "\n");
      output = ele.innerText;
    })
    .catch((err) => {
      console.error(err);
      output = "Error:\n" + err.toString();
    });
};
</script>

<style>
#app {
  font-family: "Rubik", Helvetica, Arial, sans-serif;
  margin-top: 65px;
}
h2 {
  margin-left: 15px;
  display: inline-block;
  background-image: linear-gradient(
    to top,
    rgba(82, 0, 68, 0.15) 54%,
    transparent 54%,
    transparent 100%
  );
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
footer {
  background: #280033;
  font-size: 12px;
  min-height: 50px;
  text-align: center;
  color: #fff;
}
footer > div {
  height: 100%;
  padding: 18px 0;
}
#github {
  margin: 14px 18px 0;
  padding-top: 10px;
  border-top: 1px solid #656e78;
  font-weight: 700;
}
#github > a,
#github > a:visited {
  color: #ffc500;
  text-decoration: none;
}
#github > a:hover {
  color: #fff;
}
</style>
