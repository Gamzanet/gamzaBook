---
icon: bullseye-arrow
---

# Introduction

Uniswap V4에서 추가되는 주요기능 중 Hook이라는 기능은 유동성 추가, 제거, 토큰 교환, 유동성 기부 등의 동작 시 개발자가 동작 전 후로 비즈니스 로직을 적용할 수 있는 기능입니다.

Uniswap V4는 유동성을 PoolKey를 기준으로 관리하고 PoolKey에는 교환될 토큰의 주소 2개, 수수료, 틱의 간격, 구현된 Hook Contract의 주소가 포함됩니다.

저희 프로젝트에서는 Uniswap V4를 분석하여 Hook이 적용된 유동성을 이용할 때 발생할 수 있는 위협을 정의하고 분석하는 솔루션을 제작하였습니다.

해당 솔루션은 이용자가 Hook Contract를 작성해 Uni Chain에 배포한 뒤 유동성 풀에 해당하는 PoolKey를 입력하면 해당 Hook Contract를 동적과 정적으로 각각 분석해 발생 가능한 위협을 보여주는 역할을 합니다.

동적의 경우 총 N개의 범주에서 M개의 테스트가 진행되고 정적의 경우 N개의 범주에서 M개의 테스트가 진행한 뒤 결과를 판단해 출력합니다.

Uniswap에서도 infinite hackathon, retro program 등의 활동을 통해서 Uni Chain 및 Blockchain 생태계에 대해 발전을 위해 많은 노력을 기울이고 있습니다.

우리는 Uniswap V4 이용자, Uniswap V4의 Hook 개발자가 보다 안전한 Hook Contract를 개발에 도움을 주는 것을 목표로 하고 있습니다.













<figure><img src="https://gitbookio.github.io/onboarding-template-images/quickstart-hero.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Want to learn about writing content from scratch? Head to the [Basics](https://github.com/GitbookIO/onboarding-template/blob/main/getting-started/broken-reference/README.md) section to learn more.
{% endhint %}

### Import

GitBook supports importing content from many popular writing tools and formats. If your content already exists, you can upload a file or group of files to be imported.

<div data-full-width="false">

<figure><img src="https://gitbookio.github.io/onboarding-template-images/quickstart-import.png" alt=""><figcaption></figcaption></figure>

</div>

### Sync a repository

GitBook also allows you to set up a bi-directional sync with an existing repository on GitHub or GitLab. Setting up Git Sync allows you and your team to write content in GitBook or in code, and never have to worry about your content becoming out of sync.
