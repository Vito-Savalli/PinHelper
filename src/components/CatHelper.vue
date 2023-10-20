<template>
  <div class="main-container">
    <div class="nav">
    <div @click="logAlt()">🐱</div>
    <div>🐶</div>
    <div>☕</div>
    <div>🎨</div>
  </div>
    <!-----------------1-SECTION-FIRST-1------------------->
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
        <label for="">hashtag</label>
        <select v-model="selectedTag2Choice">
          <option value="tag2Concept">Concept</option>
          <option value="tag2Cute">Cute</option>
          <option value="tag2Color">Color</option>
          <option value="defaultTag2">Default</option>
        </select>
        <label for="">keyword</label>
        <select v-model="selectedChoice">
          <option value="keywordCute">Cute</option>
          <option value="keywordPhoto">Photo</option>
          <option value="keywordIllus">Illustr</option>
          <option value="keywordTat">Tattoo</option>
        </select>
      </div>
      <div>
      <div class="colors" v-if="selectedTag2Choice === 'tag2Color'">
        <div>
        <label for="inputNblack">black</label>
        <input min="0" type="number" v-model="inputNblack" id="inputNblack" />
      </div>
        <div>
    <label for="inputNwhite">white</label>
    <input min="0" type="number" v-model="inputNwhite" id="inputNwhite" />
  </div>
        <div>

    <label for="inputNorange">orang</label>
    <input min="0" type="number" v-model="inputNorange" id="inputNorange" />
  </div>
        <div>
    <label for="inputNgrey">grey</label>
    <input min="0" type="number" v-model="inputNgrey" id="inputNgrey" />
  </div>
</div>
   
  </div>

    </section>
    <!-----------------1-SECTION-FIRST-1------------------->
    <!-----------------2-SECTION-SECOND-2------------------->
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
    <!-----------------2-SECTION-SECOND-2------------------->
    <!-----------------3-SECTION-THIRD-3------------------->
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
    <!-----------------3-SECTION-THIRD-3------------------->
    <!-----------------4-SECTION-FOURTH-4------------------->
    <section class="fourth">
      <div>
        <p class="outputTitle">{{ outputTitle[selectedIndex] }}</p>
        <p class="outputMain">{{ outputMain[selectedIndex] }}</p>
        <p class="outputAlt">{{ outputAltArr[selectedIndex] }}</p>
        <p class="outputErr" v-if="outputMain.length !== inputN">{{ outputMain.length }}|{{ inputN }}</p>
      </div>
      <div>
        <div>
          <button @click="nextCard()">&#8594</button>
          <button @click="copyToClipboard('title')">T</button>
          <button @click="copyToClipboard('main')">D</button>
          <button @click="copyToClipboard('alt')">A</button>
        </div>
      </div>
    </section>
    <div class="card-container">
  <div
    v-for="(__, index) in outputMain"
    :key="index"
    class="card"
    :class="[cardColors[index], { 'selected-card': index === selectedIndex }]"
    @click="selectCard(index)"
  >
    <div class="card-content">{{ index + 1 }}</div>
  </div>
</div>
    <!-----------------4-SECTION-FOURTH-4------------------->
    <!-----------------5-SECTION-FIFTh-5------------------->
    <section class="fifth">
      <button @click="actionDescription">DESCRIPTIONS</button>
      <p>{{ selectedIndex }}</p>
      <button @click="actionTitle">TITLE</button>
      <p>
        Urban elegance meets feline grace: Dive into a cityscape enriched by a
        cat's charisma. | Metropolitan marvel: Witness a cute cat blending
        seamlessly with city vibes and vistas. | Whiskered wanderer: A charming
        cat's escapade amidst city lights and streets. | City tales told through
        feline eyes: An adorable cat’s perspective of the buzzing urban life. |
        Concrete and cuteness combined: A city-dwelling kitty captured amidst
        skyscrapers' allure. | Streets, skyscrapers, and whiskers: A
        heartwarming city snapshot with our feline friend. | The purrfect blend
        of urban hustle and feline serenity: A cat's city journey captured. |
        City chronicles and cat tales: Experience the magic of urban life with a
        feline twist. | Feline finesse in a metropolitan setting: A captivating
        scene of a city cat's adventures.
      </p>
    </section>
    <!-----------------5-SECTION-FIFTh-5------------------->
  </div>
  <DataCat ref="dataComp" />
</template>

<script>

import DataCat from '../components/Data/DataCat.vue'

export default {
  components: {
DataCat,
  },
  data() {
    return {
      cta: [],
      tag1: "",
      tag2: [""],
      tag2Concept: [""],
      tag2Cute: [""],
      tag2Color: [""],
      tag2White: [""],
      tag2Black: [""],
      tag2Orange: [""],
      tag2Grey: [""],

      // KEYWORD
      keyword: [],
      keywordCute: [""],
      keywordPhoto: [""],
      keywordIllus: [""],
      keywordTat: [""],
      // KEYWORD
      input: "",
      inputTitle: "",
      inputBoard: "",
      inputBoardKeyword: "",
      inputHash: "#CatPoster",
      inputMain: "",
      inputAlt: "",
      inputN: 9,
      inputLong: 160,
      inputNwhite: 0,
      inputNblack: 0,
      inputNgrey: 0,
      inputNorange: 0,
      inputNbicolor: 0,
      boardPrompt: null,
      mainPrompt: null,
      titlePrompt: null,
      output: "",
      outputMain: [],
      outputTitle: [],
      outputAlt: [],
      outputAltArr: [],
      selectedIndex: 0,
      selectedTag2Choice: '',
cardColors: [],
    };
  },
  methods: {
    logAlt() {
      console.log('outputAltArr' + this.outputAltArr);
      console.log('----------------')
      console.log('outputAltArr[I]' + this.outputAltArr[this.selectedIndex]);
    },
    generateMainPrompt() {
    this.boardPrompt = null;
    this.titlePrompt = null;

    let colorDescriptions = [];
    const colorsCounts = [
        {color: 'white', count: this.inputNwhite},
        {color: 'black', count: this.inputNblack},
        {color: 'orange', count: this.inputNorange},
        {color: 'grey', count: this.inputNgrey},
    ];

    let totalColoredCats = 0;

    // WORK HERE //
    colorsCounts.forEach(colorCount => {
        if (colorCount.count > 0) {
            colorDescriptions.push(` ${colorCount.count} description${colorCount.count > 1 ? 's' : ''} of a ${colorCount.color} cat`);
            totalColoredCats += colorCount.count;
        }
    });

    let finalColorInstruction = '';
    if (colorDescriptions.length === 1) {
        finalColorInstruction = colorDescriptions[0];
    } else if (colorDescriptions.length > 1) {
        finalColorInstruction = colorDescriptions.slice(0, -1).join(', ') + ' and ' + colorDescriptions[colorDescriptions.length - 1];
    }

    if (this.inputN > totalColoredCats) {
        finalColorInstruction += `. For the rest of the descriptions, the cat color is not determined.`;
    } else {
        finalColorInstruction += '.';
    }

    this.mainPrompt = `You are expert in SEO and digital marketing strategy that drives millions of audience in Pinterest.
Create ${this.inputN} descriptions about a ${this.input}. Each description should be SEO optimized and around ${this.inputLong} character. ${this.selectedTag2Choice === "tag2Color" ? finalColorInstruction : ''} Descriptions should be not too precise so it can match any ${this.input}. ${this.inputMain + ''}description should be at least ${this.inputLong} character.
For the format: do not use quotation marks, do note add comment or other text, only provide descriptions line by line separated by this character "|".`;

    // Copy to clipboard
    this.copyToClip(this.mainPrompt);
},


    generateTitlePrompt() {
      this.mainPrompt = null;
      this.boardPrompt = null;
      this.titlePrompt = `For each descriptions, create SEO optimized title. ${this.inputTitle} Do not use quotation mark, only provide each title line by line separated by a |.`;
      this.copyToClip(this.titlePrompt);
    },
    generateBoardPrompt() {
      this.mainPrompt = null;
      this.titlePrompt = null;
      this.boardPrompt = `You are expert in SEO and digital marketing strategy that drives millions of audience in Pinterest. Create SEO optimized description for my pinterest board. ${this.inputBoard} This pinterest board is a collection of ${this.input}. description should be written in a natural human tone. description must be less than 480 character. Do not use hashtags. ${this.inputBoardKeyword}`;
      this.copyToClip(this.boardPrompt);
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
      try {
        const descriptions = await this.fetchAndSplitDescriptions();
        this.outputMain = this.modifyDescriptions(descriptions);
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
    let selectedTag2Array = [];
    let selectedKeywordArray;

    switch (this.selectedTag2Choice) {
      case "tag2Concept":
            selectedTag2Array = [...this.tag2Concept];
            this.shuffleArray(selectedTag2Array);
            break;
        case "tag2Cute":
            selectedTag2Array = [...this.tag2Cute];
            this.shuffleArray(selectedTag2Array);
            break;
        case "tag2Color":
            const colorArrays = {
                white: this.tag2White,
                black: this.tag2Black,
                orange: this.tag2Orange,
                grey: this.tag2Grey
            };
            const inputCounts = [
                {color: 'white', count: this.inputNwhite},
                {color: 'black', count: this.inputNblack},
                { color: 'orange', count: this.inputNorange },
                {color: 'grey', count: this.inputNgrey},
            ];
            inputCounts.forEach(input => {
                for (let j = 0; j < input.count; j++) {
                    selectedTag2Array.push(colorArrays[input.color][Math.floor(Math.random() * colorArrays[input.color].length)]);
                }
            });
            break;
        default:
            selectedTag2Array = [...this.tag2];
            this.shuffleArray(selectedTag2Array);
    }

    switch (this.selectedChoice) {
      case "keywordCute":
        selectedKeywordArray = this.keywordCute;
        break;
      case "keywordPhoto":
        selectedKeywordArray = this.keywordPhoto;
        break;
      case "keywordIllus":
        selectedKeywordArray = this.keywordIllus;
        break;
      case "keywordTat":
        selectedKeywordArray = this.keywordTat;
        break;
      default:
        selectedKeywordArray = this.keyword; // Default to original keyword array if none is selected
    }


this.colorCards();  // Setup the card colors based on the input

let tag2Index = 0;
this.outputAltArray = [];  // Reset the array at the start of each call

const totalColoredCats = this.inputNwhite + this.inputNblack + this.inputNorange + this.inputNgrey;

const updatedDescriptions = descriptions.map((desc, descIndex) => {
    const currentTag2 = selectedTag2Array[tag2Index] || this.tag2[Math.floor(Math.random() * this.tag2.length)];
  const randomKeyword = selectedKeywordArray[Math.floor(Math.random() * selectedKeywordArray.length)];
  const randomCTA = this.cta[Math.floor(Math.random() * this.cta.length)];

    let altText = this.inputAlt;

    if (this.selectedTag2Choice === 'tag2Color' && descIndex < totalColoredCats) {
        const currentColor = this.cardColors[descIndex % this.cardColors.length].replace('card-', '');
        altText = this.appendColorToAlt(altText, currentColor);
    }

    this.outputAltArr.push(altText);  // Save the alt text for this description

    tag2Index++;

    return `${desc} ${randomCTA} ${this.tag1} | ${currentTag2} | ${this.inputHash} | ${randomKeyword}`;
});

return updatedDescriptions;

},


 shuffleArray(array) {
    for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]]; // Swap elements
    }
},



randomFromArray(arr) {
  return arr[Math.floor(Math.random() * arr.length)];
},




    colorCards() {
  const colors = ['white', 'black', 'orange', 'grey'];  // Add or remove as per your requirement
  const inputCounts = [
    this.inputNwhite,
    this.inputNblack,
    this.inputNorange,
    this.inputNgrey
  ];

  this.cardColors = [];

  for (let i = 0; i < inputCounts.length; i++) {
    for (let j = 0; j < inputCounts[i]; j++) {
      this.cardColors.push(`card-${colors[i]}`);
    }
  }
},

    async actionTitle() {
      try {
        const titles = await this.fetchAndSplitDescriptions();
        this.outputTitle = titles;
      } catch (err) {
        console.error("Failed to read clipboard contents:", err);
      }
    },
    async copyToClipboard(type) {
      let contentToCopy = "";

      switch (type) {
        case "title":
          if (this.selectedIndex < this.outputTitle.length) {
            contentToCopy = this.outputTitle[this.selectedIndex];
          }
          break;
        case "alt":
          if (this.selectedIndex < this.outputMain.length) {
            contentToCopy = this.outputAltArr[this.selectedIndex];
          }
          break;
        case "main":
          if (this.selectedIndex < this.outputMain.length) {
            contentToCopy = this.outputMain[this.selectedIndex];
          }
          break;
        default:
          console.log("Invalid type provided");
          return;
      }

      if (contentToCopy) {
        try {
          await navigator.clipboard.writeText(contentToCopy);
          console.log("Text copied to clipboard");
        } catch (err) {
          console.error("Failed to copy text: ", err);
        }
      } else {
        console.log("No content available to copy for the provided type");
      }
    },
    copyToClip(text) {
    // Create a text area, append it to the document offscreen
    const textArea = document.createElement("textarea");
    textArea.value = text;
    textArea.style.position = 'fixed';  // Avoids scrolling to bottom of page in MS Edge
    document.body.appendChild(textArea);
    textArea.focus();
    textArea.select();

    try {
        document.execCommand('copy');  // Copy the text inside the text area
    } catch (err) {
        console.error('Failed to copy text: ', err);
    }

    document.body.removeChild(textArea);  // Remove the text area from the document
},

    selectCard(index) {
      this.selectedIndex = index;
    },
    nextCard() {
      if (this.selectedIndex == this.outputMain.length - 1) {
        this.selectedIndex = 0;
      } else {
        this.selectedIndex = this.selectedIndex + 1;
      }
    },
    appendColorToAlt(altText, color) {
    // Check if the word "cat" is present in the altText
    if(altText.includes("cat")) {
      // Replace the word "cat" with "[color] cat"
      console.log('reached');
      return altText.replace("cat", `${color} cat`);
    }
    // If "cat" is not found, just return the original altText
    return altText;
    },

    setupp() {
  this.cta = this.$refs.dataComp.cta;
  this.tag1 = this.$refs.dataComp.tag1;
  this.tag2 = [...this.$refs.dataComp.tag2];
  this.tag2Concept = [...this.$refs.dataComp.tag2Concept];
  this.tag2Cute = [...this.$refs.dataComp.tag2Cute];
  this.tag2Color = [...this.$refs.dataComp.tag2Color];
  this.tag2White = [...this.$refs.dataComp.tag2White];
  this.tag2Black = [...this.$refs.dataComp.tag2Black];
  this.tag2Orange = [...this.$refs.dataComp.tag2Orange];
  this.tag2Grey = [...this.$refs.dataComp.tag2Grey];
  this.keyword = [...this.$refs.dataComp.keyword];
  this.keywordCute = [...this.$refs.dataComp.keywordCute];
  this.keywordPhoto = [...this.$refs.dataComp.keywordPhoto];
  this.keywordIllus = [...this.$refs.dataComp.keywordIllus];
  this.keywordTat = [...this.$refs.dataComp.keywordTat]; 
    }

  },
  mounted() {
    this.setupp();
  }


  
};
</script>

<style scoped>
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
  align-items: end;
  justify-content: flex-start;
  gap: 4px
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

.fourth {
  height: 180px;
  align-items: center;
}

.fifth {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.fifth p {
  font-size: 8px;
}

.outputTitle {
  font-size: 20px;
  line-height: 1;
  margin-bottom: 5px;
}
.outputMain {
  font-size: 12px;
  line-height: 1.1;
}
.outputAlt {
  font-size: 8px;
}
.outputErr {
  font-size: 10px;
  background-color: red;
}

.card-container {
  display: flex;
  flex-wrap: wrap; /* This will allow the cards to wrap onto the next line if there are too many */
  gap: 2px; /* Provides space between the cards */
  width: 100%;
  height: 40px;
  background-color: green;
  justify-content: space-evenly;
  align-items: center;
}

.card {
  width: 20px; /* Or whatever width you'd like */
  border: 1px solid #ccc;
  height: 20px;
  border-radius: 8px; /* Rounded corners */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Optional: A little shadow for some depth */
  background-color: transparent;
  transition: transform 0.33s;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white
}

.card-content {
  display: flex;
  align-items: center;
  justify-content: center;
  line-height: 1.1;
}

.selected-card {
  background-color:transparent; /* or any color that indicates selection */
  border: 2px solid;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.3); 
  transform: scale(1.4);
  color: white;
  box-shadow: inset;
}

.card-black {
  background-color: black;
  color: white;
  border-color: white;
}

.card-white {
  background-color: white;
  color: grey;

}

.card-orange {
  background-color: rgb(254, 119, 0);
  color: white;
  border-color: white;

}

.card-grey {
  background-color: grey;
  color: white;
 
}

.colors {
  display: flex;
  flex-direction: row  !important;
  align-self: flex-end;
}

label {
  font-size: 14px;
}
</style>
