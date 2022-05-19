# React Porject - Github page 배포

> 1. npm -i gh-pages
>
> 2. package.json -> build 확인
>    (production ready -> 패키지 압축, 최적화)
>
> > - git remote -v
> >   -> repository 연결되어 있는지 확인
> > - 연결되어 있지 않다면 git init으로 초기화 설정
> > - 깃허브 페이지에서 원격 repo생성
> >
> > - git remote add origin (원격 repo 주소)
>
> 3. npm run build
> 4. build 파일 생성 확인
> 5. package.json 최하단부 바로 윗 줄에 코드 작성
>
> > -> "homepage": "http://[USERNAME].github.io/[원격repo주소]"
>
> 6. scripts part에 deploy와 predeploy 명시
>
> > - d build파일을 가져가겠다.
> >   -> "deploy": "gh-pages -d build"
> >
> > - deploy 이전에 먼저 build 파일을 만들어 줌(3번 생략 가능)
> >   -> "predeploy": "npm run build"
