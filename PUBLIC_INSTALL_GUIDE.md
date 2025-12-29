# (A안) Public 레포 기준: 레포 생성 → 배포 → 토큰 없이 설치(클론/실행)

이 문서는 “Public 레포를 만들어 배포하고, 서버에서는 GitHub 토큰 없이 `git clone`로 설치까지” 진행하는 순서를 안내합니다.

---

## 0) 중요한 사실 2가지

1) **GitHub 레포 ‘생성’은 인증이 필요**합니다.  
   - 토큰 없이(무인증) 생성은 불가능
   - 대신 `gh auth login`(device code) 같은 방식으로 “로그인 1회”로 처리 가능

2) 레포를 **Public**으로 만들면, 그 이후에는 누구나 **토큰 없이** 아래처럼 다운로드 가능  
   - `git clone https://github.com/OWNER/REPO.git`

---

## 1) Public 전환/배포 전 필수 점검

Public 레포는 인터넷 누구나 볼 수 있습니다. 아래가 포함되면 안 됩니다.

- `.env`, 토큰(ghp_), API 키(OPENAI_API_KEY), 비밀번호/시크릿
- SSH 개인키(`BEGIN OPENSSH PRIVATE KEY`)
- 인증서/키 파일(.pem/.p12/.key 등)

점검(레포 루트에서):
```bash
grep -RInE "OPENAI_API_KEY|ghp_|BEGIN OPENSSH PRIVATE KEY|password|secret|token" .
