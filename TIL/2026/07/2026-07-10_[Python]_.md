# [Python] 

> 날짜: 2026-07-10
> 원본 노션: [링크](https://app.notion.com/p/Python-Exception-3991d46c18fc8066bfa0f4527adfd00f)

---

# 🛠️ [Chapter 11]

- 지정 매칭 vs Exception ([11-13], [11-14]) : except NameError:처럼 특정 에러를 명시하면 해당 에러만 포착합니다. 모든 종류의 예외를 빠짐없이 입구 컷 하려면 최상위 예외 클래스인 except Exception:을 사용합니다.
- 에러 객체 해부 ([11-15]) : except Exception as e: 문법으로 에러 객체를 변수 e로 포착할 수 있습니다. type(e).__name__은 발생한 에러의 이름 문자열을, e는 에러의 상세 사유 메시지를 반환합니다.
- else vs finally 분기 법칙 ([11-16], [11-17]) :
```python
# [11-16-2] 예외 처리의 완전체 실행 흐름 복습
try:
    a = 10; a = b  # NameError 발생!
except NameError:
    a = 0          # 예외 포착 -> 실행 (a=0)
else:
    a += 30        # 에러가 터졌으므로 실행 스킵!
finally:
    a += 40        # 에러 여부 무관 무조건 실행! -> 최종 a = 40
```

- import vs from ... import ([11-18], [11-19]) :
- globals() 장부 검증 ([11-20]) : from 모듈 import *는 모듈 내 모든 요소를 현재 스크립트 전역 공간(globals())에 풀어버리므로, 관리 불가능한 이름 오염이 발생해 실무에서 기피하는 안티 패턴입니다.
- 점(. ) 계층 디렉토리 구조 ([11-21]) : 폴더 내부에 모듈들이 갇혀 있는 패키지 형태는 import 패키지명.모듈명 혹은 from 패키지명 import 모듈명 구조로 닷(.) 연산자를 타고 들어가 안전하게 로드합니다.
- sys.path 동적 탐색 경로 주입 ([11-21]) : 파이썬의 표준 패키지 경로 밖에 존재하는 모듈을 호출해야 할 때 사용하는 고급 경로 제어 테크닉입니다.
```python
import sys
sys.path.append(r".\my_package\files") # 1. 수동으로 외부 경로를 검색 엔진에 바인딩
import my_module2 as mm2              # 2. 경로가 뚫렸으므로 정상 임포트 완료
sys.path.pop()                        # 3. 임포트 완료 후 경로 리스트를 꺼내 장부 복구
```



