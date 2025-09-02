---
allowed-tools: (Bash:git:*)
description: git 작업용 브랜치 생성
model: claude-sonnet-4-20250514
---
1. 현재 프로그젝트와 하위 디렉토리의 프로젝트 디렉토리 마다 git의 remote의 origin을 https://github.com/changgun-lee/{프로젝트이름}.git 으로, upstream을 https://github.com/team-commdev/{프로젝트이름}.git 으로 바꿔줘
2. 'feature/$ARGUMENTS' (이)라는 이름의 브랜치를 각각 upstream과 origin에 production 브랜치를 기반으로 만들어줘. 브랜치 이름에서 빈 칸은 -으로 대치하고, 한글은 유지해야 해
3. 만든 브랜치를 upstream과 origin에 푸시해줘
3. origin의 만든 브랜치로 체크아웃해줘
