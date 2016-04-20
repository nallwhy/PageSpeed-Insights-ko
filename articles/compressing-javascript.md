# Closure Compiler로 JavaScript 압축하기

저자: Robert Bowdidge, Software Engineer
권장되는 경험: 웹페이지 제작 경험

_역자 주:_
_현재 Esmeralda Times 예제가 작동하지 않습니다._
_Closure Compiler 에 대해 더 많은 정보를 알고 싶으시면 [이 링크](https://developers.google.com/closure/compiler)를 참조하세요._


### 개요
당신의 웹페이지를 더욱 빠르게 반응하도록하는 가장 좋은 방법은 페이지가 로딩될 때 다운로드 되어야 하는 파일의 수와 크기를 줄이는 것입니다. 로딩되는 파일의 수를 줄이는 것은 브라우저의 최대 동시 다운로드 제한을 넘지 않게합니다. 파일의 크기를 줄이는 것은 모든 바이트를 인터넷을 통해 전송하기위해 드는 시간을 줄여줍니다. 이미 파일의 수와 크기를 줄여주는 몇몇 도구들이 존재합니다. 스프라이팅(spriting) 도구와 이미지 압축 도구는 당신이 이미지 파일의 수나 크기를 줄일 수 있게 해줍니다; gzip 과 HTML 압축 도구는 당신이 HTML 파일의 사이즈를 줄일 수 있게 해줍니다.

JavaScript 간결화(minimization) 도구는 총 다운로드 크기를 줄일 수 있는 다른 방법을 제공합니다. 이 툴들은 웹페이지의 JavaScript 소스 코드에 대해 동작합니다. 이 툴들은 불필요한 공백이나 주석을 제거하고, 파일의 크기를 더욱 줄이기 위해 프로그램의 변수 이름을 변경하기도 합니다. 하지만 흔히 사용되는 간결화 툴들은 코드를 더욱 압축할 수 있는 다른 방법을 놓치고 있습니다.

Closure Compiler는 새로운 간결화 툴로, 현존하는 간결화 툴들보다 더욱 JavaScript 코드를 압축하는 방법을 찾아줍니다. 이것은 JavaScript를 더 작은 형태로 재작성하는 compiler-like 기술을 통해 코드가 정확하게 동작함을 보장하면서도 추가적인 압축을 해냅니다. Closure Compiler는 몇몇 파일들을 하나의 파일로 압축할 수 있고, 이를 통해 당신의 JavaScript 크기를 쉽게 반으로 줄일 수 있습니다. Closure Compiler는 또한 당신의 프로그램에 대한 문법적 체크와 정적 분석을하여, 잠재적인 문법이나 타입 오류를 표시하고 모든 브라우저에서 잘 동작하지는 않는 코드 패턴들을 하이라이트합니다.


### 예제: Closure Compiler는 당신을 위해 무엇을 할 수 있는가?
예제를 시작하면서 당신이 Esmeralda Times라는 큰 신문을 위한 웹 개발자라고 상상해보세요. 그리고 당신은 당신의 홈페이지 코드를 최적화해보길 원합니다. [http://closure-compiler.appspot.com](http://closure-compiler.appspot.com)에 있는 Closure Compiler 웹 서비스 UI에 가보세요. 웹 어플리케이션이 간단한 Hello World 예제로 시작하고 있는 것을 확인할 수 있습니다. "Compile" 을 클릭하면 Closure Compiler가 그 코드를 간결화해서 오른쪽에 보여줍니다.

하지만 "Hello World"에는 신경쓰지말고 당신의 웹페이지 속도를 향상시키는데 신경씁시다.

이 가상의 예제(실제 미디어 웹사이트로부터 차용함)는 홈페이지가 로딩될 때 여섯 개의 JavaScript 파일을 로딩하고, 이는 총 227,000 바이트입니다. 그 중 두 개의 파일은 Esmeralda Times의 코드이고, 나머지는 Prototype과 script.aculo.us JavaScript 라이브러리를 사용합니다.

Closure Compiler 웹 서비스 UI에서 "Hello Wolrd" 부분의 코드를 지우기 위해 "Reset" 링크를 클릭하세요. URL을 텍스트 필드에 적고 "Add"를 누르거나, 특정 페이지들을 로딩하기위해 이 명시적인 요청들을 Closure Compiler 웹 서비스의 인풋 영역에 적어서 당신 홈페이지 JavaScript 파일들의 URL을 추가하세요:

```
// ==ClosureCompiler==
// @output_file_name default.js
// @compilation_level ADVANCED_OPTIMIZATIONS
// @code_url http://www.esmeraldatimes.com/sitewide/sitewide.js
// @code_url http://www.esmeraldatimes.com/sitewide/main.js
// @code_url http://www.esmeraldatimes.com/js/ext/prototype/prototype.js
// @code_url http://www.esmeraldatimes.com/js/ext/scriptaculous/scriptaculous.js?load=effects,dragdrop
// @code_url http://www.esmeraldatimes.com/js/ext/scriptaculous/effects.js
// @code_url http://www.esmeraldatimes.com/js/ext/scriptaculous/dragdrop.js
// ==/ClosureCompiler==
```

이제 컴파일 모드를 선택하세요. 다음 선택이 가능합니다:

- **Whitespace Only** 모드는 간단하게 필요없는 공백과 주석들을 제거해줍니다. "Whitespace Only" 모드를 선택하고 컴파일을 누르면, 기존 227K의 소스 코드보다 28% 작은 164K의 JavaScript 파일 하나를 보여준다.

- **Simple** 모드는 조금 더 복잡하다. 이것은 JavaScript 함수 바디를 지역 변수 이름 변경, 상수 표현들을 최종값으로 대체("1+3"을 "4"로 바꾸는 것과 같이)를 포함한 몇몇 방법을 통해 최적화한다. 하지만 당신의 JavaScript 밖에서 참조되는 어떠한 함수나 변수도 지우지 않는다. 이것은 코드를 227K에서 132K로 42% 줄인다.

- **Advanced** 모드는 당신의 코드에 보다 더 복잡한 변경을 수행합니다. "Advanced" 최적화를 선택하고 코드를 컴파일하여 그 결과를 확인해보세요. 당신의 기존 코드와 더욱 달라졌을 것입니다; 모든 함수 이름을 짧게 바꾸고, 사용되지 않는 것 같은 함수들을 삭제하고, 몇몇 함수 호출을 함수 본문으로 변경하고, 그 밖에 여러가지 최적화가 코드를 더욱 줄여줍니다. 일반적으로, 다른 곳에서 보여져야하는 함수라든지 당신의 JavaScript에서 불려야하는 다른 곳에 있는 코드라든지에 대한 추가적인 정보 없이는 JavaScript 코드에 Advanced 모드를 사용할 수 없습니다. 하지만 Advanced 모드가 코드 크기를 227K에서 86K로 기존 코드보다 62% 더 작게 줄이는 것은 주목할 만한 가치가 있습니다. 만약 이 파일이 기존의 1/3 시간만에 로딩되기를 바란다면, 변경이 정확히 일어나도록 하기 위해 Advanced 모드에 모든 정보를 넣는 것이 할만한 것임을 깨달을 수 있을 것입니다.

아래는 Esmeralda Times에서 사용된 JavaScript 파일의 최적화 결과가 어떻게 생겼을지에 대한 예제입니다:

![Closure Compiler example](https://developers.google.com/speed/images/closure-compiler-web-service.jpg)

결과로 나온 압축된 소스를 UI 내에 있는 링크를 통해 다운로드 받거나, 최적화된 JavaScript를 Closure Cimpiler 웹 서비스 UI로부터 복사 붙여넣기를 통해 당신의 소스 파일에 넣을 수 있습니다.

무엇보다 좋은 것은, 이 압축된 코드를 Closure Inspector 소스 맵을 통해 여전히 디버깅 할 수 있다는 것입니다. Firebug(역자 주: Firefox의 개발용 애드온) 디버거가 이 소스 맵을 이용해 당신이 디버깅하고 있는 최적화된 소스 코드와 연관된 원본 소스 코드에서 해당하는 라인을 표시해줍니다. Closure Inspector 소스 맵을 만드는 것은 Closure Cimpiler를 당신의 로컬 머신에서 소스나 미리 빌드된 jar 파일을 통해 구동하는 것을 필요로 합니다.

_역자 주: Closure Inspector는 [더 이상 쓰이지 않는다고 합니다](http://stackoverflow.com/questions/15961056/closure-compiler-and-closure-inspector).
Compile된 JavaScript 코드에 대한 디버깅 방법은 [이 글](http://stackoverflow.com/questions/14147479/debugging-closure-compiler-compiled-javascript/14147795#14147795)을 참조해주세요._

지금까지 Closure Compiler가 Esmeralda Times를 위해 무엇을 할 수 있는지 살펴봤습니다; 당신의 웹 어플리케이션에서 가져온 JavaScript를 보시고, Closure Cimpiler가 당신의 실제 코드를 위해 무엇을 할 수 있는지 보세요.


### Closure Compiler는 당신을 위해 무엇을 더 할 수 있는가?

Closure Compiler는 잘못된 코드에 대해서도 당신에게 경고해줄 수 있습니다. 이것이 당신의 JavaScript 코드를 파싱하기 때문에, 코드를 브라우저에 불러올 필요 없이 컴파일 에러에 대해 경고할 수 있습니다. 잘 사용하지 않는 버튼을 눌렀을 때 미스테리하게 발생하는 에러에 문법 에러는 없다는 것을 확신할 수 있습니다. Closure Compiler는 배열에 끝에 남는 콤마(`a = [1, 2, 3, ];`)와 같이 모든 브라우저에서 지속적으로 가능하지는 않은 흔한 코드 패턴들을을 확인할 수 있습니다. 위 예제는 몇몇 브라우저들에서는 배열 안에 세 개의 요소를 만들고, 몇몇은 네 개를 만듭니다; 이러한 비일관성은 몇몇 추적하기 어려운 버그들을 만들 수 있습니다. Closure Compiler는 유효하지 않은 수학 연산, 실행되지 않는 코드, 충분한 인자가 전달되지 않은 함수 호출 등도 확인할 수 있습니다.

Advance Mode에서는, Closure Compiler에서 프로그램의 로직 에러들을 찾아내기 위해 코드에 있는 타입 어노테이션을 사용할 수 있습니다 - 예를 들어 당신은 `Money` 객체를 넘기려고 했지만, 실수로 `AccountNumber` 객체를 넘긴 경우. 이것은 Java 같은 타입 언어에서와 같이 버그를 찾을 수 있는 이득을 제공하면서, 여전히 JavaScript의 빠르고 재미있는 코딩 경험을 유지해줍니다.


### Closure Compiler는 어떻게 동작하는가?

Closure Compiler는 사실 JavaScript 컴파일러이지만, 머신 코드를 만들어내는 다른 컴파일러들과는 다르게 유효한 JavaScript 코드를 만들어냅니다. 이것은 여러가지 흥미로운 방법들로 JavaScript 코드를 재작성할 수 있습니다. 이것은 `(15 * 280) + 16`을 `4216`으로 변경하는 식으로, 상수 표현들을 확인하고 이를 상수 값으로 변경합니다. 이렇게 함으로써, 15 글자를 5 글자로 줄입니다. 더욱 중요하게, 이것은 당신에게 코드를 깔끔하고 이해하기 쉬운 방법으로 작성할 수 있는 자유를 주고, 코드의 최종 크기에 대한 걱정으로부터 자유로울 수 있게 합니다. 한두군데에서만 불리는 코드를 인라인으로 바꾸어서(함수 호출을 함수 바디의 내용으로 대체), 함수 선언에 필요한 공간을 절약합니다. Closure Compiler는 gzip 압축이 더 잘되도록 하기 위해, 동시에 사용되지 않는 두 가지 다른 변수가 있을 때 같은 이름을 공유하게 하여 가능한 많은 변수들이 매우 짧은 이름을 쓸 수 있도록 합니다.

Closure Compiler는 오픈소스입니다; 당신 스스로 이것을 빌드하고 자신의 JavaScript 코드 최적화를 작성하기 위해 [http://code.google.com/closure/compiler/](http://code.google.com/closure/compiler/)에서 소스를 실험하거나 다운로드 받을 수 있습니다.

_역자 주: Github [https://github.com/google/closure-compiler](https://github.com/google/closure-compiler)로 변경되었습니다._

### 결론

Closure Compiler는 JavaScript 개발자에게 JavaScript 코드를 압축할 수 있는 새롭고 더 좋은 방법을 제공하면서, JavaScript를 사용하는 당신의 웹 페이지가 그 어떤 방법보다도 더 빠르게 로딩될 수 있게 해줍니다. 당신의 JavaScript 소스에 적용해보고, 이것이 어떤 차이를 만들어 내는지 확인해보세요. 