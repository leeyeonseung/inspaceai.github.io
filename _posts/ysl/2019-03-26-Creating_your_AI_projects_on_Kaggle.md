---
layout: post
title: "Ben Hamner의 Createing your AI projects on Kaggle 번역"
author: "이연승"
date: 2019-03-26 18:00:00
categories: [Tutorials, Kaggle]
tags: [Kaggle]
---

본 포스트에서는 \[Kaggle의 Ben Hamner가 쓴글에대한 번역\]자료를 살펴보겠습니다.

---

# Kaggle에서 AI 프로젝트 생성하기

Kaggle은 모든 AI프로젝트들을 통합하여 생성할수 있는 플랫폼이 되고자 합니다. 지난분기에, 많은 새로운 기능을 출시하고 컴퓨터 리소스를 확장하여 플랫폼에 구축할 수 있는 작업 범위와 폭을 늘렸습니다.

이제 작업 중인 개인 데이터셋을 로드하고, 클라우드 기반 데이터 과학 환경에서 해당 데이터셋에 대한 복잡한 분석을 개발하며, 프로젝트를 재현 가능한 방식으로 공동작업자와 공유할 수 있습니다.

## Kaggle에 개인의 데이터셋 업로드하기

Kaggle은 최초로 Kaggle Kernels와 데이터셋이 모두 공유되어야 하는 제도를 시작하였습니다. 우리는 작년 6월에 사용자들이 개인의 Kaggle Kernel을 만들 수 있도록 하였습니다. 이것은 많은 Kaggle 사용자들을 변화시켯습니다 : 그 후 생성된 94%의 Kernel들이 개인적인 것이었습니다.

하지만 여기서 끝이 아닙니다 : 사용자들은 공개된 데이터에서 Kernel을 작동시키는데 한계를 느꼇을것입니다. 이러한 상황은 사용자 개인의 프로젝트가 Kaggle에서 사용되는데 제한되었을것입니다.

지난분기에, Kaggle은 개인의 데이터셋을 출시하였습니다. 이를 통해 개인 데이터셋을 Kaggle에 업로드하고 Kernel에서 Python 또는 R 코드를 실행할 수 있습니다. 사용자는 최대 20GB 할당량까지 무제한의 개인 데이터셋 업로드가 가능합니다. 모든 새 데이터셋은 기본적으로 개인 데이터로 설정됩니다. www.kaggle.com/datasets의 "New Dataset"을 클릭하거나 Kernel editor의 데이터 탭에서 "Upload a Dataset"를 클릭하여 데이터 세트를 생성할 수 있습니다.

![개인데이터셋추가]({{ "/images/ysl/upload_privatedataset.png" | prepend: site.baseurl }})

개인 데이터셋을 만들고 나면 1월에 출시해 3월에 확장한 Kaggle API를 통해 새로운 버전을 게시하여 계속 업데이트할 수 있습니다. 이 API를 사용하면 명령줄에서 데이터를 다운로드하고 대회 제품을 제출할 수 있습니다.

## Kaggle Kernels의 새로운 editing experience

이제 당신은 개인의 데이터셋을 창조하고 그것을 Kaggle Kernels에 올릴 수 있습니다.

Kaggle Kernels는 클릭 한 번으로 클라우드에서 interactive 할수있는 Python/R 코딩 세션을 만들 수 있게 해줍니다. 이러한 코딩 세션은 Docker container서 실행되며, 많은 Python 및 R 분석환경을 포함하여 버전 처리된 컴퓨팅 환경을 제공합니다.

Kernel을 사용하는 두가지 방식이 있습니다. : interactive와 batch입니다. interactive하는 부분은 라이브 부분에서 Python 또는 R 코드를 쓸 수 있게 함으로서, 코드 선택을 실행하고 출력을 바로 볼 수 있습니다. 세션이 완료되면 "Commit & Run"을 클릭하여 코드 버전을 저장하고 깨끗한 환경에서 batch 버전을 Top-to-bottom으로 실행할수있습니다. 사용자는 랩탑을 끄고 돌아다니더라도 cloud에서 batch는 완료될것입니다.

돌아오면 당신이 만든 모든 batch 실행에 대한 완전한 버전 기록을 갖게 될 것입니다. 세션이 끝날 때 "Commit & Run"을 수행하지 않은 경우, 최신 편집 내용은 다음에 Kernel을 편집할 때 볼 수 있는 작업 초안으로 저장됩니다.

Kaggle은 항상 노트북을 interactive 모드로 사용했고 이번 분기에 스크립트에 대한 interactive모드의 지원을 시작했습니다. interactive형 스크립트와 함께, 우리는 Kaggle Kernels의 스크립트 및 노트북 편집기를 업데이트하고 통합했습니다. 이렇게 하면 콘솔에 접근할 수 있고, 세션에 현재 있는 변수를 표시하며, interactive 세션에서 현재 컴퓨팅 사용량을 볼 수 있습니다. 또한, interactive세션은 많은 흥미로운 미래확장을 위한 토대를 마련합니다.

## Kaggle Kernel에서 더욱 복잡한 프로젝트 만들기

우리는 지난 분기에 당신이 Kaggle Kernels에서 할 수 있는 일의 확장에 초점을 맞추었습니다. 개인 데이터를 사용할 수 있도록 지원하는 것도 이 중 하나였습니다.

우리는 Kaggle Kernels의 compute 한계를 1시간에서 6시간으로 확대했습니다. 따라서 실행할 수 있는 모델과 분석할 수 있는 데이터셋의 크기와 복잡성이 증가합니다. 이러한 확장된 compute 제한은 interactive 세션과 batch 세션 모두에 적용됩니다. Kernel에 custom packages를 설치하는 기능을 추가했습니다. Kernel editor의 "Setting" 탭에서 이 작업을 수행할 수 있습니다. Python에서 PyPI 또는 GitHub의 패키지에 대해 "pip install" 명령을 실행하십시오. R의경우에는  GitHub의 패키지에 대해 "devtools::install_github" 명령을 실행하십시오. 이러한 일은 추가된 패키지를 포함하도록 기본 contatiner를 확장합니다. 이 사용자 정의 container에서 후속 kernel fork/edits를 실행하면 여러분과 다른 사람들이 여러분의 결과를 더 쉽게 재현하고 구축할 수 있도록 합니다.

![복잡한프로젝트만들기]({{ "/images/ysl/makecomplex.png" | prepend: site.baseurl }})

또한, Kaggle은 Kaggle Kernels의 견고함을 향상시키는데 초점을 맞추었습니다. Kaggle이 한일들은 Kernel을 좀더 안정적이고 매끄럽게 변화시킬 것입니다. 여기서 무슨 문제가 생기면 [Kaggle](https://www.kaggle.com/product-feedback)에게 알려주세요.

## 공동작업자와 프로젝트를 공유하세요

데이터셋을 업로드하거나 Kernel을 작성하여 새 프로젝트를 시작하면 공동작업자와 작업을 공유할 수 있습니다. 이러한 일들은 그들이 당신의 프로젝트를 보고, 논평하고, 구축할 수 있게 해줄 것입니다.

![프로젝트공유]({{ "/images/ysl/shareproject.png" | prepend: site.baseurl }})
뷰어 또는 편집자로 공동작업자를 추가할 수 있습니다.

데이터셋의 뷰어는 데이터에 대한 커널을 보고 다운로드하고 쓸 수 있다. 또한, 편집자는 새로운 데이터 세트 버전을 생성할 수 있다.

커널의 뷰어들은 Kernel을 보고 나눌 수 있습니다. 모든 기본 데이터셋에 액세스할 수 있는 경우 복제 및 확장도 가능합니다. Kernel editor들은 Kernel을 직접 편집하여 새로운 버전을 만들 수 있습니다.

Kernel을 대회 팀의 일부로 생성할 때 Kernel은 기본적으로 다른 팀과 공유됩니다. Kaggle은 많은 대회 팀들이 서로 다른 컴퓨팅 환경 때문에 협력하는 데 어려움을 겪었다고 알고있습니다만 이것을 통해 대회에서 협업하는것이 쉬워지길 기대하고있습니다.

## 추가적인 업데이트

Kaggle에서 몇가지 추가로 업데이트 한것들이 있습니다. 우리는 고객이 분석과 머신러닝과 데이터시각화에 대한 실제 경험을 쌓을 수 있도록 빠르고 체계적인 방법으로 [Kaggle Learn](https://www.kaggle.com/learn/overview)을 출시했습니다. 여기에는 몇가지의  튜토리얼과 브라우저에서 완료할 수 있는 6개의 트랙에 걸친 연습이 포함되어 있다. 우리는 [두 번째 Kernel 대회](https://www.kaggle.com/c/mercari-price-suggestion-challenge)를 마쳤고, 이 대회에서 모든 출품작들은 Kernel을 통해 만들어져야 했습니다. Kaggle은 2384팀이나 참가하는 참여율에 깜짝 놀랐습니다. 이 새로운 대회 형식에 대한 [피드백](https://www.kaggle.com/c/mercari-price-suggestion-challenge/discussion/45129)에 감사합니다. Kaggle은 컴퓨팅 기능을 [모델 복잡성에 믿을 수 없을 정도로 효과적으로 조직화하는것](https://www.kaggle.com/c/mercari-price-suggestion-challenge/discussion/50256)으로 제한하는 것을 연구했습니다. 또한 Kaggle은 변동이 심한 컴퓨팅 성능을 포함하여 유일한 형식의 Kernel에 대한 불만을 연구하였습니다. 전반적으로, 향후 이 대회 형식을 귀하의 의견을 토대로 개선하여 반복하는 것을 목표로 합니다.

Kaggle은 [BigQuery Public Datasets](https://www.kaggle.com/datasets)에 대한 통합을 시작했고, 이는 커널의 [GitHub Repos](https://www.kaggle.com/github/github-repos)와 [비트코인 블록체인](https://www.kaggle.com/bigquery/bitcoin-blockchain) 같은 더 크고 복잡한 데이터셋을 문의 할 수 있게 해줍니다.

많은 분들이 이전에 출판한 콘텐츠에 대한 더 많은 통제와 삭제 능력을 원한다고 말해 주셨습니다. 이제 사용자들은데이터 세트, 커널, 주제 및 Kaggle에 작성한 설명을 삭제할 수 있습니다. 이것들은 [[삭제된] 기록](https://www.kaggle.com/deleted-dataset/949)을 남기기 때문에 관련된 커널이나 코멘트는 여전히 어떤 맥락을 가지고 있습니다.

데이터셋, 대회 및 커널을 주제별로 쉽게 탐색할 수 있도록 하기 위해 Kaggle에 대한 다양한 주제에 대한 [개요 페이지](https://www.kaggle.com/tags)를 발행했습니다.

원본 \([https://towardsdatascience.com/creating-your-ai-projects-on-kaggle-ff49f679f611](https://towardsdatascience.com/creating-your-ai-projects-on-kaggle-ff49f679f611)\)

이글은 원작성자의 번역 동의를 받았습니다.
