# Jira Recently Assigned Issues Command

내게 할당되고 아직 수정되지 않았고, 작업 시작 전인 Jira 이슈를 최근 수정된 순서대로 10개 조회하는 명령어

## Usage

```bash
# 이 명령어를 Claude Code에서 실행
```

## Command Implementation

```javascript
// Atlassian 리소스 정보 조회
const resources = await mcp__atlassian__getAccessibleAtlassianResources();
const cloudId = resources[0].id; // estsoft.atlassian.net

// 내 계정 정보 확인
const userInfo = await mcp__atlassian__atlassianUserInfo();

// JQL 쿼리: 내게 할당되고 OPEN 상태인 이슈를 최근 수정순으로 조회
const jqlQuery = "project = ROUNZ and assignee = currentUser() AND resolution = Unresolved AND statusCategory = \"To Do\" ORDER BY updated DESC";

// Jira 이슈 검색 실행
const searchResult = await mcp__atlassian__searchJiraIssuesUsingJql({
    cloudId: cloudId,
    jql: jqlQuery,
    maxResults: 10,
    fields: ["summary", "description", "status", "created", "updated"]
});

// 결과 출력
if (searchResult.issues && searchResult.issues.length > 0) {
    console.log(`🎯 내게 할당된 OPEN 상태 이슈 ${searchResult.issues.length}개:`);
    
    searchResult.issues.forEach((issue, index) => {
        console.log(`\n${index + 1}. ${issue.key}: ${issue.fields.summary}`);
        console.log(`   상태: ${issue.fields.status.name}`);
        console.log(`   수정일: ${new Date(issue.fields.updated).toLocaleString('ko-KR')}`);
        console.log(`   생성일: ${new Date(issue.fields.created).toLocaleString('ko-KR')}`);
        if (issue.fields.description) {
            const desc = issue.fields.description.substring(0, 100);
            console.log(`   설명: ${desc}${desc.length >= 100 ? '...' : ''}`);
        }
        console.log(`   URL: https://estsoft.atlassian.net/browse/${issue.key}`);
    });
} else {
    console.log("✅ 현재 할당된 OPEN 상태의 이슈가 없습니다.");
}
```

## JQL Query Explanation

- `assignee = currentUser()`: 현재 사용자(나)에게 할당된 이슈
- `resolution = Unresolved`: 아직 수정하지 않은 이슈만
- `statusCategory = \"To Do\"`: 작업 시작 전 이슈만 (Open 상태)
- `ORDER BY updated DESC`: 최근 수정된 순서대로 정렬

## Account Information

- 사용자: 이창근 (gilchris@estsoft.com)
- Atlassian 인스턴스: estsoft.atlassian.net
- 계정 ID: 557058:f3c61b2b-61b5-47f9-b220-ebf980c7ea3e
