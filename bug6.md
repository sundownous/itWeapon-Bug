6일차
브랜치 관련 명령어들

알고 가야 할것들
1.커밋하면 커밋 객체가 생김 커밋 객체에는 부모 커밋에 대한 참조와 실제 커밋을 구성하는 파일 객체가 있음
2.브랜치는 논리적으로 어떤커밋과 그 조상들을 묶어서 뜻하지만 사실은 객체커밋 하나만 뜻함 
브랜치를 사용할때
-1새로운 기능 추가 마스터브랜치에는 정상적으로 작동하는 안정적인 버전의 프로젝트가 있으므로 새 기능을 추가할때 마스터브랜치의 최신커밋에서 브랜치를 만들어개발하고 문제가 없으면 병합
-2버그수정 버그가 발생하면 마스터브랜치에서 새 브랜치를 생성해서 작업 충돌주의
-3병합과 리베이스 테스트 임시브랜치를 만들어서 테스트 해바라 이상있으면 브랜치 삭제
-4 이전코드 개선 
-5특정 커밋으로 돌아가고 싶을땨 hard reset이나 revert를 써도 되지;민 브랜치를 새로만들어도 된다

명령어들

git branch [-v]:로컬저장소의 브핸치를 보는 명령 -v옵션은 마지막 커밋도 표현 HEAD브랜치는*가 붙어있다

git branch [-f] <브랜치이름> [커밋체크섬]: 새로운 브랜치를 생성 커밋체크섬 값을 안주면 HEAD로 부터 새로운 브랜치를 생성 이미있는 브랜치를 다른커밋으로 옮기고싶으면 -f옵션을 줘야해

git branch -r[v]:원격저장소의 브랜치를 보고싶을때 -v옵션을통해 커밋요약도 가능

git checkout <브랜치이름>:특정 브랜치로 체크아웃할태 사용 

git branch -b <브랜치이름> [커밋체크섬]:특정 커밋에서 브랜치를 생성하고 체크아웃까지 한다

git merge <대상브랜치>: 현재브랜치와 대상브랜치를 병합 병합커밋이 생기는 경우가 많다

git rebase <대상브랜치>:내 브랜치의 커밋을 대상브랜치에 재배치시김 

git branch -d:특정브랜치를 삭제할때 사영 헤드브랜치나 병합되지 않은건 삭제불가

git branxh -D:강제삭제

git reset --hard <이동할 커밋 체크섬>: 현재브랜치를 지정한 커밋으로 이동 작업폴더의 내용도 같이 변경
커밋체크섬을 HEAD~ 또는 HEAD^로 대체가능
HEAD~ <숫자> HEAD ~n은 n번쩨 조상커밋이라는뜻 1은 부모 2는할아버지
HEAD^ <숫자> 모두 부모커밋이지만 HEAD^2는 두번째 부모 커밋이다 병합커밋처럼 부모가 둘 이상인 커밋에서 의미가 있다

git tag -a -m <간단한 메시지><테그이름>[브랜치 또는 체크섬]:-a로 주석있는 테그를 생성 메시지와 테그이름은 핈고 브랜치이름을 생략하면 HEAD에 테그를 생성
git push <원격저장소 별명> <태그이름>:원격저장소에 태그를 업로드

rebase 주의사항
원격저장소에 푸시한 브랜치는 rebase안하는게 원칙 c1커밋을 원격에 푸시하고 rebase하면 원격에는 c1ㅣ 존재하고 로컬에는 c1,커밋이 생성 근데 다른 누군가는 원격에 있는 c1을 병합할 수 있다 언젠가는 변경된 c1,커밋도 원격에 푸시되고 원격에는 같은 커밋이였던 c1과 c1,커밋이 동시에 존재 이거 해결하겠다고 merge나 rebase를 또 사용하면 더 꼬이는거지