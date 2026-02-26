class Zalgo {
  constructor() {
    this.__options = {
      top: true,
      middle: true,
      bottom: true,
      maxHeight: 15,
      randomization: 100
    };

    this.__middle = Array.from({length: 5}, (_, i) => String.fromCharCode(820 + i));

    this.__top = [
      ...Array.from({length: 22}, (_, i) => String.fromCharCode(768 + i)),
      ...Array.from({length: 8}, (_, i) => String.fromCharCode(829 + i)),
      String.fromCharCode(836),
      String.fromCharCode(838), String.fromCharCode(842), String.fromCharCode(843),
      String.fromCharCode(844), String.fromCharCode(848), String.fromCharCode(849),
      String.fromCharCode(850), String.fromCharCode(855), String.fromCharCode(856),
      String.fromCharCode(859), String.fromCharCode(861), String.fromCharCode(861),
      String.fromCharCode(864), String.fromCharCode(865),
    ];

    this.__bottom = [
      ...Array.from({length: 28}, (_, i) => 790 + i)
        .filter(i => i !== 794 && i !== 795)
        .map(i => String.fromCharCode(i)),
      ...Array.from({length: 4}, (_, i) => String.fromCharCode(825 + i)),
      String.fromCharCode(837), String.fromCharCode(839), String.fromCharCode(840),
      String.fromCharCode(841), String.fromCharCode(845), String.fromCharCode(846),
      String.fromCharCode(851), String.fromCharCode(852), String.fromCharCode(853),
      String.fromCharCode(854), String.fromCharCode(857), String.fromCharCode(858),
      String.fromCharCode(860), String.fromCharCode(863),
    ];
  }

  get [Symbol.toStringTag]() {
    return "zalgo";
  }

  toString() {
    return "[object zalgo]";
  }

  encode(text) {
    let result = "";
    for (const char of text) {
      let newChar = char;
      if (this.__options.middle) newChar += this.__pick(this.__middle);
      if (this.__options.top)    newChar += this.__diacritics(this.__top);
      if (this.__options.bottom) newChar += this.__diacritics(this.__bottom);
      result += newChar;
    }
    return result;
  }

  decode(text) {
    return [...text].filter(c => {
      const code = c.charCodeAt(0);
      return code < 768 || code > 865;
    }).join("");
  }

  setMaxHeight(value) {
    const v = Number(value);
    if (v < 0 || v > 300) throw new RangeError(`maxHeight must be between 0 and 300, got ${v}`);
    this.__options.maxHeight = v;
  }

  __pick(arr) {
    return arr[Math.floor(Math.random() * arr.length)];
  }

  __diacritics(arr) {
    const len = this.__options.maxHeight -
      Math.random() * ((this.__options.randomization / 100) * this.__options.maxHeight);
    let str = "";
    for (let i = 0; i < len; i++) {
      str += arr[Math.floor(Math.random() * (arr.length - 1))];
    }
    return str;
  }
}

module.exports = new Zalgo();
