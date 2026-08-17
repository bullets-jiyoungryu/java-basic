# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

IntelliJ IDEA의 기본 Java 프로젝트 템플릿에서 생성된 최소 구성의 저장소다. 현재 소스는 `src/Main.java` 한 개뿐이며, 커밋 이력도 초기 커밋(`2e5550f`) 하나다.

**빌드 도구가 없다.** Maven(`pom.xml`)도 Gradle(`build.gradle`)도 없고, 외부 의존성·테스트 프레임워크도 설정되어 있지 않다. 컴파일은 IntelliJ 모듈 설정(`java-basic.iml`) 또는 `javac`에 직접 의존한다.

## 빌드 및 실행

JDK 17(프로젝트 SDK: `zulu-17`, language level `JDK_17`)을 기준으로 한다.

```bash
# 컴파일 (IntelliJ와 동일한 출력 경로 사용)
javac -d out/production/java-basic src/Main.java

# 실행
java -cp out/production/java-basic Main
```

`out/`은 `.gitignore` 대상이므로 커밋하지 않는다.

## 테스트

테스트 소스 디렉터리와 테스트 프레임워크가 존재하지 않는다. 테스트를 추가하려면 JUnit 등의 의존성 도입과 함께 빌드 구성(Maven/Gradle 도입 또는 `.iml`의 `sourceFolder` 추가)을 먼저 결정해야 하며, 이는 사용자와 합의할 사항이다. 임의로 빌드 도구를 도입하지 않는다.

## 구조상 유의점

- 소스 루트는 `src/`이며 **패키지 디렉터리가 없다.** `Main`은 default package에 속한다. 클래스를 추가할 때 패키지를 도입할지 여부는 기존 구조(default package)와의 일관성을 고려해 판단한다.
- `.idea/` 설정은 저장소에 커밋되어 있다(`misc.xml`, `modules.xml`, `google-java-format.xml`, `vcs.xml`). 단 `workspace.xml` 등은 `.idea/.gitignore`로 제외된다. 프로젝트 SDK나 language level 변경은 `.idea/misc.xml` 수정으로 이어지며 커밋 대상이 된다.
- google-java-format 플러그인은 **비활성** 상태다(`.idea/google-java-format.xml`의 `enabled=false`). 자동 포매팅에 의존하지 말고 기존 코드 스타일(4-space 인덴트)을 따른다.
- `src/Main.java`의 주석은 IntelliJ가 생성한 안내용 TIP 주석이다(`<shortcut>`, `<icon>` 태그 포함). 실제 코드 설명이 아니므로 새 코드의 주석 스타일 기준으로 삼지 않는다.
