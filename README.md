# 프론트엔드 배포 파이프라인

## 개요

![Untitled](./hanghaeplus-4-1.drawio.svg)

GitHub Actions에 워크플로우를 작성해 다음과 같이 배포가 진행되도록 합니다.

(사전작업: Ubuntu 최신 버전 설치)

1. Checkout 액션을 사용해 코드 내려받기
2. `npm install` 명령어로 프로젝트 의존성 설치
3. `npm run build` 명령어로 Next.js 프로젝트 빌드
4. AWS 자격 증명 구성
5. 빌드된 파일을 S3 버킷에 동기화
6. CloudFront 캐시 무효화

## 주요 링크

- S3 버킷 웹사이트 엔드포인트: http://hanghaeplus-4-1-jaytee.s3-website.ap-northeast-2.amazonaws.com/
- CloudFront 배포 도메인 이름: https://d2dfpuvcgi7z5t.cloudfront.net/

## 주요 개념

## 주요 개념

- GitHub Actions과 CI/CD 도구:
  -- GitHub Actions는 GitHub 리포지토리에서 CI/CD 파이프라인을 자동화할 수 있는 도구입니다.
  이를 통해 코드 변경 사항을 자동으로 테스트하고 빌드하며 배포할 수 있습니다.
  CI/CD는 Continuous Integration(지속적 통합)과 Continuous Deployment(지속적 배포)를 의미하며, 개발과 배포 과정을 자동화하여 효율성을 높입니다.

- S3와 스토리지:
  -- Amazon S3(Simple Storage Service)는 AWS에서 제공하는 객체 스토리지 서비스로,
  대규모 데이터를 안전하게 저장하고 관리할 수 있습니다.
  S3 버킷은 파일을 저장하는 컨테이너 역할을 하며, 웹사이트 호스팅, 백업, 데이터 아카이빙 등 다양한 용도로 사용됩니다.

- CloudFront와 CDN:
  -- Amazon CloudFront는 AWS에서 제공하는 콘텐츠 전송 네트워크(CDN) 서비스로,
  전 세계에 분산된 엣지 로케이션을 통해 사용자에게 콘텐츠를 빠르고 안전하게 전달합니다.
  CloudFront는 웹사이트, 동영상 스트리밍, API 등을 가속화하는 데 사용됩니다.

- 캐시 무효화(Cache Invalidation):
  -- 캐시 무효화는 CDN이나 웹 브라우저에 저장된 캐시된 콘텐츠를 최신 버전으로 갱신하는 과정입니다.
  CloudFront에서 캐시 무효화를 수행하면, 특정 경로의 콘텐츠가 변경되었을 때 이를 즉시 반영하여 사용자에게 최신 콘텐츠를 제공할 수 있습니다.
  관련 코드는 .github/workflows/deployment.yml 파일 내 Invalidate CloudFront cache를 참고할 수 있습니다.

- Repository secret과 환경변수:
  -- Repository secret은 GitHub 리포지토리에 저장된 민감한 정보를 보호하기 위해 사용됩니다.
  예를 들어, AWS 자격 증명이나 API 키와 같은 정보를 secret으로 저장하여 워크플로우에서 안전하게 사용할 수 있습니다.
  환경변수는 실행 환경에서 설정된 변수로, 코드 실행 시 필요한 설정 값을 동적으로 제공할 수 있습니다.
