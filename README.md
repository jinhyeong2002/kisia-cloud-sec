
# KISIA Cloud Security Lab

  KISIA 클라우드 보안 실습 과정에서 사용한 Kubernetes, DevSecOps, 보안 정책,
  SBOM 관련 실습 파일을 정리한 저장소입니다.

  ## 프로젝트 개요

  이 저장소는 클라우드 네이티브 환경에서 보안 설정을 실습하기 위한 예제 파일들을
  포함합니다.

  주요 실습 내용은 다음과 같습니다.

  - Kubernetes Pod 및 Deployment 보안 설정
  - 잘못된 Pod 설정과 개선된 Pod 설정 비교
  - OPA Gatekeeper 기반 정책 적용
  - 이미지 Pull 정책 및 Label 필수화 정책 실습
  - SBOM 파일 관리
  - GitHub Actions 기반 DevSecOps 파이프라인 구성
  - CodeQL, Snyk, Dependabot 등 보안 자동화 설정

  ## 디렉터리 구조

  ```text
  .
  ├── .github/
  │   ├── dependabot.yml
  │   └── workflows/
  │       ├── codeql.yml
  │       ├── github-actions-demo.yml
  │       └── security.yml
  ├── day3/
  │   ├── bad-pod.yaml
  │   ├── good-pod.yaml
  │   ├── good-pod-validate.yaml
  │   ├── constraint-owner.yaml
  │   ├── constrainttemplate-requiredlabels.yaml
  │   ├── policy-imagepull-always.yaml
  │   ├── policy-require-labels.yaml
  │   ├── cosign.pub
  │   ├── sbom.cdx.json
  │   ├── sbom.spdx.json
  │   └── kisia-cloud-sec/
  │       ├── index.js
  │       ├── package.json
  │       ├── dockerfile
  │       └── sbom.cdx.json
  ├── 3-pod.yaml
  ├── 3-pod-fixed.yaml
  ├── baseline-compliance.yaml
  ├── nginx-deploy.yaml
  ├── template.yaml
  └── 클라우드 보안 실습 파일/

  ## 주요 파일 설명

   파일                                       설명
  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   3-pod.yaml                                 기본 Pod 예제 파일
  ─────────────────────────────────────────  ───────────────────────────────────
   3-pod-fixed.yaml                           보안 설정이 개선된 Pod 예제
  ─────────────────────────────────────────  ───────────────────────────────────
   baseline-compliance.yaml                   보안 기준 준수 관련 YAML
  ─────────────────────────────────────────  ───────────────────────────────────
   nginx-deploy.yaml                          Nginx Deployment 예제
  ─────────────────────────────────────────  ───────────────────────────────────
   template.yaml                              클라우드 리소스 구성 템플릿
  ─────────────────────────────────────────  ───────────────────────────────────
   day3/bad-pod.yaml                          보안 설정이 부족한 Pod 예제
  ─────────────────────────────────────────  ───────────────────────────────────
   day3/good-pod.yaml                         보안 설정이 적용된 Pod 예제
  ─────────────────────────────────────────  ───────────────────────────────────
   day3/good-pod-validate.yaml                정책 검증용 Pod 예제
  ─────────────────────────────────────────  ───────────────────────────────────
   day3/policy-imagepull-always.yaml          이미지 Pull 정책 예제
  ─────────────────────────────────────────  ───────────────────────────────────
   day3/policy-require-labels.yaml            Label 필수화 정책 예제
  ─────────────────────────────────────────  ───────────────────────────────────
   day3/constrainttemplate-                   OPA Gatekeeper ConstraintTemplate
   requiredlabels.yaml
  ─────────────────────────────────────────  ───────────────────────────────────
   day3/constraint-owner.yaml                 OPA Gatekeeper Constraint
  ─────────────────────────────────────────  ───────────────────────────────────
   day3/sbom.cdx.json                         CycloneDX 형식 SBOM
  ─────────────────────────────────────────  ───────────────────────────────────
   day3/sbom.spdx.json                        SPDX 형식 SBOM
  ─────────────────────────────────────────  ───────────────────────────────────
   .github/workflows/codeql.yml               CodeQL 정적 분석 워크플로
  ─────────────────────────────────────────  ───────────────────────────────────
   .github/workflows/security.yml             보안 검사 자동화 워크플로
  ─────────────────────────────────────────  ───────────────────────────────────
   .github/dependabot.yml                     의존성 업데이트 자동화 설정

  ## DevSecOps 예제 앱

  day3/kisia-cloud-sec 디렉터리에는 간단한 Node.js 기반 DevSecOps 실습용 애플리
  케이션이 포함되어 있습니다.

  cd day3/kisia-cloud-sec
  npm install
  node index.js

  Docker 이미지 빌드 예시:

  docker build -t kisia-cloud-sec -f dockerfile .

  ## Kubernetes 실습 예시

  Pod 생성:

  kubectl apply -f 3-pod.yaml

  보안 설정이 적용된 Pod 생성:

  kubectl apply -f 3-pod-fixed.yaml

  Nginx Deployment 생성:

  kubectl apply -f nginx-deploy.yaml

  ## OPA Gatekeeper 정책 적용 예시

  ConstraintTemplate 적용:

  kubectl apply -f day3/constrainttemplate-requiredlabels.yaml

  Constraint 적용:

  kubectl apply -f day3/constraint-owner.yaml

  정책 검증용 Pod 적용:

  kubectl apply -f day3/good-pod-validate.yaml

  ## GitHub Actions 보안 자동화

  이 저장소는 다음과 같은 GitHub Actions 기반 보안 자동화 구성을 포함합니다.

  - CodeQL을 이용한 정적 코드 분석
  - Snyk 기반 보안 취약점 점검
  - Dependabot을 통한 의존성 업데이트 자동화
  - GitHub Actions Workflow 실습

  ## 보안 주의사항

  개인키와 민감 정보는 Git에 포함하지 않습니다.

  현재 저장소에서는 다음 유형의 파일을 .gitignore로 제외합니다.

  .DS_Store
  *.pem
  *.key

  예를 들어 다음 파일들은 업로드 대상에서 제외됩니다.

  - cfn-lab-key.pem
  - day3/cosign.key

  ## 사용 목적

  이 저장소는 클라우드 보안 및 DevSecOps 실습 자료 관리 목적으로 사용됩니다.

  실습 주제:

  - Kubernetes 보안 설정
  - Policy as Code
  - 컨테이너 이미지 보안
  - SBOM 생성 및 관리
  - CI/CD 보안 자동화
  - GitHub 기반 보안 워크플로 구성

  ## Repository

  GitHub 저장소:

  https://github.com/jinhyeong2002/kisia-cloud-sec
