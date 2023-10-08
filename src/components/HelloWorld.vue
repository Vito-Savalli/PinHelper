<template>
  <div class="main-container">
    <!------------------SECTION-FIRST-------------------->
    <section class="first">
      <div>
        <label for="inputN">N</label>
        <input min="0" step="3" type="number" v-model="inputN" id="inputN" />
      </div>
      <div>
        <label for="inputLong">Long</label>
        <input
          min="0"
          step="10"
          type="number"
          v-model="inputLong"
          id="inputLong"
        />
      </div>
      <div>
        <label for="inputIsConcept">Concept</label>
        <input type="checkbox" v-model="inputIsConcept" id="inputIsConcept" />
      </div>
      <div>
        <label for="inputIsCute">Cute</label>
        <input type="checkbox" v-model="inputIsCute" id="inputIsCute" />
      </div>
      <div>
        <label for="inputIsColor">Color</label>
        <input type="checkbox" v-model="inputIsColor" id="inputIsColor" />
      </div>
      <div v-if="inputIsColor">
        <label for="inputNblack">black</label>
        <input type="number" v-model="inputNblack" id="inputNblack" />
      </div>
      <div v-if="inputIsColor">
        <label for="inputNwhite">white</label>
        <input type="number" v-model="inputNwhite" id="inputNwhite" />
      </div>
      <div v-if="inputIsColor">
        <label for="inputNorange">orange</label>
        <input type="number" v-model="inputNorange" id="inputNorange" />
      </div>
      <div v-if="inputIsColor">
        <label for="inputNgrey">grey</label>
        <input type="number" v-model="inputNgrey" id="inputNgrey" />
      </div>
    </section>
    <!------------------SECTION-FIRST-------------------->
    <!------------------SECTION-SECOND-------------------->
    <section class="second">
      <div>
        <textarea v-model="input" id="input"></textarea>
      </div>
      <div>
        <label for="inputAlt">Alt</label>
        <input type="text" v-model="inputAlt" id="inputAlt" />
        <label for="inputHash">#</label>
        <input type="text" v-model="inputHash" id="inputHash" />
      </div>
    </section>
    <!------------------SECTION-SECON-------------------->
    <!------------------SECTION-THIRD-------------------->
    <section class="third">
      <div>
        <button @click="generateMainPrompt">Main Prompt</button>
        <input type="text" v-model="inputMain" id="inputMain" />
      </div>
      <div>
        <button @click="generateTitlePrompt">Title Prompt</button>
        <input type="text" v-model="inputTitle" id="inputTitle" />
      </div>
      <div>
        <button @click="generateBoardPrompt">Board Prompt</button>
        <input type="text" v-model="inputBoardKeyword" id="inputBoardKeyword" />
      </div>
    </section>
    <!------------------SECTION-THIRD-------------------->
    <!------------------SECTION-FOURTH-------------------->
    <section>
      <div>
        <p>
          Urban elegance meets feline grace: Dive into a cityscape enriched by a
          cat's charisma. | Metropolitan marvel: Witness a cute cat blending
          seamlessly with city vibes and vistas. | Whiskered wanderer: A
          charming cat's escapade amidst city lights and streets. | City tales
          told through feline eyes: An adorable cat’s perspective of the buzzing
          urban life. | Concrete and cuteness combined: A city-dwelling kitty
          captured amidst skyscrapers' allure. | Streets, skyscrapers, and
          whiskers: A heartwarming city snapshot with our feline friend. | The
          purrfect blend of urban hustle and feline serenity: A cat's city
          journey captured. | City chronicles and cat tales: Experience the
          magic of urban life with a feline twist. | Feline finesse in a
          metropolitan setting: A captivating scene of a city cat's adventures.
        </p>
        <p>{{ outputMain[1] }}</p>
        <p>{{ outputMain.length }}</p>
      </div>
      <div>
        <div>
          <button @click="actionDescription">DESCRIPTIONS</button>
          <button @click="actionTitle">TITLE</button>
        </div>
        <div><button>A</button><button>A</button><button>A</button></div>
      </div>
    </section>
    <!------------------SECTION-FOURTH-------------------->
    <!------------------SECTION-FIFTh-------------------->
    <section class="fifth"></section>
    <!------------------SECTION-FIFTh-------------------->
  </div>
</template>

<script>
export default {
  data() {
    return {
      cta: "This is the CTA template.",
      tag1: "#AmazingCatArt",
      tag2: ["#exampleTag2_1", "#exampleTag2_2", "#exampleTag2_3"], // You can adjust these example tags
      keyword: ["exampleKeyword1", "exampleKeyword2", "exampleKeyword3"], // You can adjust these example keywords
      input: "",
      inputTitle: "",
      inputBoard: "",
      inputBoardKeyword: "",
      inputHash: "#CatPoster",
      inputMain: "",
      inputAlt: "",
      inputN: 6,
      inputLong: 160,
      inputNwhite: 0,
      inputNblack: 0,
      inputNgrey: 0,
      inputNorange: 0,
      inputNbicolor: 0,
      inputIsConcept: false,
      inputIsColor: false,
      inputIsCute: false,
      boardPrompt: null,
      mainPrompt: null,
      titlePrompt: null,
      output: "",
      outputMain: [],
    };
  },
  methods: {
    generateMainPrompt() {
      this.boardPrompt = null;
      this.titlePrompt = null;
      this.mainPrompt = `You are expert in SEO and digital marketing strategy that drives millions of customers.
Create ${this.inputN} description about a ${this.input}. Each description should be SEO optimized and around ${this.inputLong} character. Descriptions should be not to precise so it can match any ${this.input}. ${this.inputMain}
For the format: do not use quotation mark, only provide descriptions line by line.`;
    },
    generateTitlePrompt() {
      this.mainPrompt = null;
      this.boardPrompt = null;
      this.titlePrompt = `For each descriptions, create SEO optimized title. ${this.inputTitle} Do not use quotation mark, only provide each title line by line.`;
    },
    generateBoardPrompt() {
      this.mainPrompt = null;
      this.titlePrompt = null;
      this.boardPrompt = `You are expert in SEO and digital marketing strategy that drives millions of audience. Create SEO optimized description for my pinterest board. ${this.inputBoard} This pinterest board is a collection of ${this.input}. description should be in a natural human tone. description should be around 460 character. Do not use hashtags. ${this.inputBoardKeyword}`;
    },

    generateOutputMain() {
      this.outputMain = `description + CTA + + keyword`;
    },

    generateOutpuTitle() {
      this.outputTitle = `title`;
    },

    generateOutputAlt() {
      this.outputALt = `alt`;
    },
    async actionDescription() {
      console.log("test");
      try {
        const descriptions = await this.fetchAndSplitDescriptions();
        this.outputMain = this.modifyDescriptions(descriptions);
        console.log(this.outputMain);
      } catch (err) {
        console.error("Failed to read clipboard contents:", err);
      }
    },

    async fetchAndSplitDescriptions() {
      const clipboardContent = await navigator.clipboard.readText();
      return clipboardContent
        .split("|")
        .map((desc) => desc.trim())
        .filter(Boolean);
    },

    modifyDescriptions(descriptions) {
      return descriptions.map((desc) => {
        const randomTag2 =
          this.tag2[Math.floor(Math.random() * this.tag2.length)];
        const randomKeyword =
          this.keyword[Math.floor(Math.random() * this.keyword.length)];

        return `${desc} ${this.cta} ${this.tag1} | ${randomTag2} | ${this.inputHash} | ${randomKeyword}.`;
      });
    },
    actionTitle() {
      // Process GPT and deliver
    },
  },
};
</script>

<style scoped>
/* Add your styling here */

button {
  padding: 10px 15px;
  background-color: #007bff;
  border: none;
  color: #fff;
  cursor: pointer;
  border-radius: 5px;
}

button:hover {
  background-color: #0056b3;
}

.main-container {
  display: flex;
  flex-direction: column;
  width: 100vw;
  max-width: 100vw;
  height: 100vh;
}

section {
  display: flex;
  border: 1px solid red;
  width: 100%;
  max-height: 400px;
  padding: 10px 20px;
}

textarea {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

#inputAlt {
  width: 70%;
}

#inputHash {
  width: 30%;
}

.first {
  display: flex;
  align-items: center;
  justify-content: flex-start;
}

.first div {
  display: flex;
  flex-direction: column;
}

.second {
  flex-direction: column;
  gap: 10px;
}

.second > div:nth-of-type(2) {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.third {
  gap: 20px;
}

.third div {
  width: 33%;
}

.third div input,
.third div button {
  width: 100%;
}

.fifth {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.fifth p {
  font-size: 8px;
}

input[type="number"] {
  font: 20px;
  width: 40px;
  height: 40px;
}

input[type="text"] {
  font: 30px;
  width: 60px;
}
</style>
