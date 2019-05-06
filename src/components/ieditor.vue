
<template lang="html">
  <input v-bind:type="type" v-bind:class="editorClass" v-bind:value="value" v-on:input="input();" v-bind:maxlength="maxLength">
</template>

<script>
export default {
  data() {
    var value = '';
    var type = 'text';
    var editorClass = 'ieditor';
    var realValue = '';
    var maxLength = null;
    return {
      value, type, editorClass, realValue, maxLength
    }
  },
  created () {
    var patterns = '[ZZZ-ZZ-ZZZZZZZ, ZZZZZZ-ZZZZZZZ]'.split(',');
		patterns[0] = patterns[0].replace(/[\[\]]/g, '').trim(); // 첫번째 패턴에서 배열기호를 제거한 실제 패턴
		patterns[1] = patterns[1].replace(/[\[\]]/g, '').trim(); // 두번째 패턴에서 배열기호를 제거한 실제 패턴
    this.maxLength = patterns[0].length > patterns[1].length ? patterns[0].length : patterns[1].length;
  },
  methods: {
    input () {
        var elem = this.$el;
				var splitter = '-'; // 추후 splitter를 설정할 수 있도록 변수처리
				var value = this.$el.value; // input에서 출력되는 실제ㅔ 값
				// 출력된 값에서 패턴이 제거된 실제 값을 저장한다.
				var realValue = elem.value.replace(new RegExp(eval('/' + splitter + '/g')), '');
				// var patterns = elem.pattern.split(','); // 멀티패턴처리
        var patterns = '[ZZZ-ZZ-ZZZZZZZ, ZZZZZZ-ZZZZZZZ]'.split(',');
				var pattsLen = patterns.length; // 패턴의 개수
				var firstPatternLen = 0, secondPatternLen = 0; // 추후 3가지이상 패턴이 필요할수도있으니 그때를대비한 명명
				var objPattern;

				patterns[0] = patterns[0].replace(/[\[\]]/g, '').trim(); // 첫번째 패턴에서 배열기호를 제거한 실제 패턴
				firstPatternLen = patterns[0].replace(/(\W)/g, '').trim().length; // 첫번째 패턴에서 특수기호를 제거한 실제 패턴의 길이
				objPattern = this.getExpFromPattern(patterns[0], splitter); // 첫번째 패턴을 토대로 정규식과 변환식을 리턴받음
        this.realValue = realValue;

				if(patterns.length > 1) {
					// 일단 패턴이 최대 두개라는 가정하에. 추후3개이상인 경우 반복문 처리해야 할듯
					patterns[1] = patterns[1].replace(/[\[\]]/g, '').trim();
					secondPatternLen = patterns[1].replace(/(\W)/g, '').trim().length;
					// 두번째 패턴의 길이가 짧고 실제 값이 두번째 패턴 길이보다 크면 첫번째 패턴값을 적용
					// 첫번째 패턴의 길이가 짧고 실제 값이 첫번째 패턴 길이보다 크면 두번째 패턴값을 적용
					if(firstPatternLen > secondPatternLen && this.realValue.length > secondPatternLen) {
						objPattern = this.getExpFromPattern(patterns[0], splitter);
					} else if (firstPatternLen < secondPatternLen && this.realValue.length > firstPatternLen) {
						objPattern = this.getExpFromPattern(patterns[1], splitter);
					}
				}
				// 출력값에 실제값을 정규식 변환한 내용을 저장한다.
				elem.value = this.realValue.replace(objPattern.regExp, objPattern.repExp);
    },
    getExpFromPattern (pattern, splitter) {
				var _pattern = pattern.split(splitter);
				var _pattLen = _pattern.length;
				var strExp = [];
				var repExp = [];
        var _strReg;

				var len = this.realValue.length;
				var currPattern = [];

				for(var i = 0; i < _pattLen; i++) {
					var charPatt = 'Z'; // 영문인경우 A 숫자인경우 Z. 일단 Z로 하드코딩 해둠. 추후 변수처리
					switch(charPatt) {
						case 'Z':
							if(i === 0) { // 첫번째 패턴 영역인 경우 무조건 전체 길이를 받아옴
								_strReg = '(\\d{' + _pattern[i].length + '})';
								strExp.push(_strReg);
								repExp.push('$' + (i + 1));
							} else { // 그 외엔 앞에 1, 패턴길이로 받아옴
								_strReg = '(\\d{1,' + _pattern[i].length + '})';
								strExp.push(_strReg);
								repExp.push('$' + (i + 1));
							}
							currPattern.push(_pattern[i]);
							break;
						case 'A':
							break;
					}
					// 실제 입력된 값이 현재 길이보다 짧다면 패턴을 만들면 안되므로 break;
					if(len <= currPattern.join('').length) {
						break;
					}
				}
				return { // 정규식과 $1-$2-$3같은 변환식을 만들어서 리턴
					regExp: new RegExp(eval('/' + strExp.join('') + '/g')),
					repExp: repExp.join(splitter)
				}
    }
  }
}
</script>

<style lang="css" scoped>
</style>
