# ModPilot Lite — static V1

Fabric 모드 30~150개 정도를 빠르게 관리하기 위한 단일 페이지 웹앱.

## 구현된 기능

- Fabric `.jar` 여러 개 일괄 드래그앤드롭 / 선택
- `fabric.mod.json` 파싱
- mod id, 이름, 버전, 설명, 작성자, 아이콘
- `depends / recommends / suggests / conflicts / breaks`
- SHA-1 기반 Modrinth 정확 매칭
- 목표 Minecraft 버전 + Fabric 지원 여부 확인
- 업데이트 가능 여부
- ON/OFF
- ON/OFF, 업데이트, 지원 상태, 이름, 버전 정렬
- 이름/mod ID/버전/메모 검색
- 빠른 필터
- 커스텀 태그 + 색상
- 태그 포함 필터
- Shift+태그 클릭으로 제외 필터
- 메모
- 대체 모드 이름/링크
- Required By 역종속성
- Missing dependency / conflict 표시
- OFF/삭제 전 직접·간접 영향 경고
- Compact/Normal 행
- 다중 선택
- Shift 범위 선택
- Ctrl+A 현재 필터 전체 선택
- 일괄 ON/OFF/태그 추가/삭제
- History
- 개별 add/delete/edit Undo
- IndexedDB 자동 저장
- JSON Export/Import 백업

## 업데이트 확인 방식

이름 검색으로 억지 매칭하지 않아.

1. JAR의 SHA-1 계산
2. Modrinth `/v2/version_files`에서 파일 해시 정확 매칭
3. 해당 프로젝트의 목표 Minecraft 버전 + Fabric 버전 목록 조회
4. 현재 JAR 자체가 목표 버전을 지원하면 `최신/호환`
5. 다른 목표 버전용 릴리스가 있으면 `업데이트 가능`
6. 목표 버전용 릴리스가 없으면 `미지원`
7. Modrinth 해시 매칭이 안 되면 `미확인`

## V1 제한

- Fabric만 지원
- CurseForge 연동 없음
- 계정/클라우드 없음
- Prism Launcher 직접 연동 없음
- 라이브러리 자동 판별 없음
- dependency 버전 범위의 완전한 SemVer 판정은 아직 하지 않음
- 일괄 작업은 History에 남지만 원자적 Undo는 아직 지원하지 않음
- Modrinth에 등록되지 않은 JAR은 자동 검색해서 추측하지 않음

## 추천 사용 순서

1. Target에 `26.3` 같은 목표 버전 입력
2. mods 폴더의 JAR을 전부 드래그
3. `업데이트 확인`
4. `미지원`, `업데이트`, `문제` 필터로 정리
5. 필요한 모드에 태그/메모/대체 모드 기록
6. 작업 전후로 Export해서 JSON 백업
