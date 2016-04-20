# PageSpeed Insights에 관해
Page Speed Insights는 모바일 기기와 데스크탑 기기에서의 페이지의 성능을 측정합니다. Url을 모바일 유저 에이전트에 한 번, 데스크탑 유저 에이전트에 한 번해서 두 번 불러옵니다.

PageSpeed Score는 0부터 100 포인트까지의 범위입니다. 점수가 높을 수록 좋고 85점 이상의 점수는 페이지의 성능이 좋은 편이라는 것을 의미합니다. PageSpeed Insights는 계속해서 발전하고 있기 때문에 우리가 새 룰을 추가하거나 분석을 개선함에 따라 점수가 변할 수 있다는 것을 유의해주세요.

PageSpeed Insights는 페이지의 성능이 어떻게 향상될 수 있을지 측정합니다:
- 처음 페이지에 보이는 영역([above-the-fold](http://whatis.techtarget.com/definition/above-the-fold)) 로딩까지의 시간: 사용자가 새 페이지를 요청하고부터 처음 페이지에 보이는 영역의 콘텐츠가 브라우저에 렌더링되기까지 소요된 시간.
- 완전한 페이지 로딩까지의 시간: 사용자가 새 페이지를 요청하고부터 페이지가 완전히 브라우저에 렌더링되기까지 소요된 시간.

하지만 네트워크 연결의 성능이 상당히 다양하기 때문에, PageSpeed Insights는 페이지의 성능 중 네트워크에 독립적인 면만 고려합니다: 서버 설정, 페이지의 HTML 구조, 이것이 사용하는 이미지, JavaScript, CSS 등의 외부 리소스들. 제안대로 구현하면 페이지의 상대적인 성능은 증가할 것입니다. 하지만 페이지의 절대적인 성능은 여전히 사용자의 네트워크 연결에 영향을 받을 것입니다.

각각의 제안은 중요도를 나타내기위해 우선사항 표시로 평가됩니다.

| Icon | Name | Description |
| --- | --- | --- |
| ![red](https://developers.google.com/speed/docs/insights/images/exclamation.png) | 빨간 느낌표 | 이것을 고치는 것은 눈에 띌만한 성능 향상을 가져올 것입니다. |
| ![yellow](https://developers.google.com/speed/docs/insights/images/exclamation_yellow.png) | 노란 느낌표 | 어렵지 않다면 고치는 것을 고려해보세요. |
| ![green](https://developers.google.com/speed/docs/insights/images/check.png) | 녹색 체크 | 별 다른 이슈가 없습니다. 잘하셨어요! |

PageSpeed Insights 에 대한 우리의 가장 최근 업데이트는 모바일 성능에 초점을 두고 있습니다. [PageSpeed Insights에서의 모바일 분석](./mobile.md)이나 ~~[Google I/O 2013 on Instant Mobile Websites](https://developers.google.com/events/io/sessions/325128936)~~에서 더 많은 정보를 확인하실 수 있습니다.

PageSpeed Insights에 의해 수행된 분석의 전체 결과를 보는데도 아마 관심이 있을 것 같습니다.

## 피드백을 보내주세요
PageSpeed Insights에 대해 피드백을 보내주시면 감사하겠습니다. 테스팅 도구나 우리가 권장하는 best practice들에 대해 제안이 있으시다면 [pagespeed-insights-discuss](https://groups.google.com/forum/#!forum/pagespeed-insights-discuss)에 올려주세요.

## 질문이 있으신가요?
PageSpeed Insights에 대한 질문이 있으시다면, 저희 [FAQ](https://developers.google.com/speed/docs/insights/faq)를 참조하시거나 [discussion group](https://groups.google.com/forum/#!forum/pagespeed-insights-discuss)에 메시지를 올려주세요.