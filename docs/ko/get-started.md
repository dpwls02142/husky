# 시작하기

## 설치하기

::: code-group

```shell [npm]
npm install --save-dev husky
```

```shell [pnpm]
pnpm add --save-dev husky
```

```shell [yarn]
yarn add --dev husky
# 패키지가 private이 아닌 경우에만 pinst를 추가하세요
yarn add --dev pinst
```

```shell [bun]
bun add --dev husky
```

:::

## `husky init` (추천)

`init` 명령어는 프로젝트에 husky를 설정하는 과정을 간소화 합니다. 이 명령은 `.husky/` 디렉터리에 `pre-commit` 스크립트를 생성하고, `package.json`의 `prepare` 스크립트를 업데이트 합니다. 이후에는 워크플로우에 맞게 수정할 수 있습니다.

::: code-group

```shell [npm]
npx husky init
```

```shell [pnpm]
pnpm exec husky init
```

```shell [yarn]
# yarn은 다른 패키지 매니저들과 차이점이 있으므로
# "사용 방법" 섹션을 참고하세요.
```

```shell [bun]
bunx husky init
```

:::


## 테스트

축하합니다! 단 한 줄의 명령어로 첫 번째 Git hooks 설정을 마쳤습니다 🎉. 이제 테스트해봅시다:

```shell
git commit -m "Keep calm and commit"
# 이 커밋 시, test 스크립트가 실행됩니다
```

## 몇 가지 안내...

### 스크립트 작성

보통은 `npm run` 이나 `npx` 명령어만 훅에서 실행해도 충분하지만, 더 복잡한 워크플로우가 필요하다면 POSIX 셸 스크립트를 직접 작성할 수도 있습니다.

예를 들어, 외부 의존성 없이 스테이징된 파일을 커밋할 때마다 자동으로 린트하는 방법은 다음과 같습니다:

```shell
# .husky/pre-commit
prettier $(git diff --cached --name-only --diff-filter=ACMR | sed 's| |\\ |g') --write --ignore-unknown
git update-index --again
```

이것은 기본적으로 동작하는 예시입니다. 더 발전된 기능이 필요하다면 [lint-staged](https://github.com/lint-staged/lint-staged) 를 참고하세요.

### 훅 비활성화 하기

Husky는 Git 훅 사용을 강제하지 않습니다. 전역적으로 (`HUSKY=0`) 환경 변수를 이용해 비활성화할 수 있고, 필요한 경우에만 선택적으로 사용할 수도 있습니다. 수동 설정 등 자세한 내용은 [사용 방법](how-to) 섹션을 참고하세요.