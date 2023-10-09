modifyDescriptions(descriptions) { return descriptions.map((desc) => { let
selectedTag2Array; let selectedKeywordArray; // Logic to determine the tag2
array based on dropdown value switch (this.selectedTag2Choice) { case
"tag2Concept": selectedTag2Array = this.tag2Concept; break; case "tag2Cute":
selectedTag2Array = this.tag2Cute; break; case "tag2Color": selectedTag2Array =
this.tag2Color; break; default: selectedTag2Array = this.tag2; // Default to
original tag2 array } // Logic to determine the keyword array based on dropdown
value switch (this.selectedChoice) { case "keywordCute": selectedKeywordArray =
this.keywordCute; break; case "keywordPhoto": selectedKeywordArray =
this.keywordPhoto; break; case "keywordIllus": selectedKeywordArray =
this.keywordIllus; break; case "keywordTat": selectedKeywordArray =
this.keywordTat; break; default: selectedKeywordArray = this.keyword; // Default
to original keyword array if none is selected } const randomTag2 =
selectedTag2Array[ Math.floor(Math.random() * selectedTag2Array.length) ]; const
randomKeyword = selectedKeywordArray[ Math.floor(Math.random() *
selectedKeywordArray.length) ]; return `${desc} ${this.cta} ${this.tag1} |
${randomTag2} | ${this.inputHash} | ${randomKeyword}.`; }); },
