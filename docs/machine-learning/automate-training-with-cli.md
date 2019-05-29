---
title: ML.NET CLI를 통한 모델 학습 자동화
description: ML.NET CLI 도구를 사용하여 명령줄에서 자동으로 최상의 모델을 학습하는 방법을 알아봅니다.
author: CESARDELATORRE
ms.date: 04/17/2019
ms.custom: how-to
ms.openlocfilehash: 33383582140d9df4290a0bbf30659301af837d1d
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65065896"
---
# <a name="automate-model-training-with-the-mlnet-cli"></a><span data-ttu-id="11cee-103">ML.NET CLI를 통한 모델 학습 자동화</span><span class="sxs-lookup"><span data-stu-id="11cee-103">Automate model training with the ML.NET CLI</span></span>

<span data-ttu-id="11cee-104">ML.NET CLI는 ML.NET을 학습할 때 .NET 개발자들에게 ML.NET에서의 "자유를 더합니다”.</span><span class="sxs-lookup"><span data-stu-id="11cee-104">The ML.NET CLI "democratizes" ML.NET for .NET developers when learning ML.NET.</span></span>

<span data-ttu-id="11cee-105">ML.NET API를 (ML.NET AutoML CLI 없이) 그대로 사용하려면 트레이너(특정 작업에 대한 기계 학습 알고리즘 구현)와 데이터에 적용할 데이터 변환 세트(기능 엔지니어링)를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-105">To use the ML.NET API by itself, (without the ML.NET AutoML CLI) you need to choose a trainer (implementation of a machine learning algorithm for a particular task), and the set of data transformations (feature engineering) to apply to your data.</span></span> <span data-ttu-id="11cee-106">최적 파이프 라인은 데이터 세트마다 다르며 모든 선택에서 최적의 알고리즘을 찾으려는 시도는 복잡성을 더합니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-106">The optimal pipeline will vary for each dataset and selecting the optimal algorithm from all the choices adds to the complexity.</span></span> <span data-ttu-id="11cee-107">나아가 각각의 알고리즘에는 조정 대상인 하이퍼 매개 변수 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-107">Even further, each algorithm has a set of hyperparameters to be tuned.</span></span> <span data-ttu-id="11cee-108">따라서 몇 주, 때에 따라서는 몇 달에 걸쳐 기계 학습 모델 최적화를 수행하여 기능 엔지니어링, 학습 알고리즘, 하이퍼 매개 변수의 최적 조합을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-108">Hence, you can spend weeks and sometimes months on machine learning model optimization trying to find the best combinations of feature engineering, learning algorithms, and hyperparameters.</span></span>

<span data-ttu-id="11cee-109">이 프로세스는 ML.NET AutoML 인텔리전트 엔진을 구현하는 ML.NET CLI를 통해 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-109">This process can be automated with the ML.NET CLI, which implements the ML.NET AutoML intelligent engine.</span></span> 

> [!NOTE]
> <span data-ttu-id="11cee-110">이 항목은 현재 미리 보기로 제공되는 ML.NET **CLI** 및 ML.NET **AutoML**을 참조하며, 자료는 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-110">This topic refers to ML.NET **CLI** and ML.NET **AutoML**, which are currently in Preview, and material may be subject to change.</span></span> 

## <a name="what-is-the-mlnet-command-line-interface-cli"></a><span data-ttu-id="11cee-111">ML.NET CLI(명령줄 인터페이스)란?</span><span class="sxs-lookup"><span data-stu-id="11cee-111">What is the ML.NET Command-line Interface (CLI)?</span></span>

<span data-ttu-id="11cee-112">모든 명령 프롬프트(Windows, Mac 또는 Linux)에서 ML.NET CLI를 실행하여 학습 데이터 세트를 기초로 품질 높은 ML.NET 모델과 소스 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-112">You can run the ML.NET CLI on any command-prompt (Windows, Mac, or Linux) for generating good quality ML.NET models and source code based on your training dataset.</span></span>

<span data-ttu-id="11cee-113">아래 그림에서처럼 간단하게 품질 높은 ML.NET 모델(직렬화된 모델 .zip 파일)과 샘플 C# 코드를 생성하여 해당 모델을 실행/채점할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-113">As shown in the figure below, it is simple to generate a high quality ML.NET model (serialized model .zip file) plus the sample C# code to run/score that model.</span></span> <span data-ttu-id="11cee-114">또한, 모델 생성/학습을 위한 C# 코드도 생성되므로 이렇게 생성된 “최상의 모델”에 사용되는 알고리즘과 설정을 바탕으로 연구 및 반복을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-114">In addition, the C# code to create/train that model is also generated, so that you can research and iterate on the algorithm and settings used for that generated "best model".</span></span> 

<span data-ttu-id="11cee-115">![이미지](media/automate-training-with-cli/cli-high-level-process.png "ML.NET CLI 내 AutoML 엔진 작업")</span><span class="sxs-lookup"><span data-stu-id="11cee-115">![image](media/automate-training-with-cli/cli-high-level-process.png "AutoML engine working inside the ML.NET CLI")</span></span>

<span data-ttu-id="11cee-116">직접 코딩하지 않고도 자체 데이터 세트에서 해당 자산을 생성할 수 있기 때문에 ML.NET을 이미 알고 있더라도 생산성이 증대됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-116">You can generate those assets from your own datasets without coding by yourself, so it also improves your productivity even if you already know ML.NET.</span></span>

<span data-ttu-id="11cee-117">현재 ML.NET CLI에서 지원되는 ML 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-117">Currently, the ML Tasks supported by the ML.NET CLI are:</span></span>

- `binary-classification`
- `multiclass-classification` 
- `regression`
- <span data-ttu-id="11cee-118">앞으로 `recommendation`, `ranking`, `anomaly-detection`, `clustering` 같은 다른 기계 학습 작업도 지원될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-118">Future: other machine learning tasks such as `recommendation`, `ranking`, `anomaly-detection`, `clustering`</span></span>

<span data-ttu-id="11cee-119">사용 예:</span><span class="sxs-lookup"><span data-stu-id="11cee-119">Example of usage:</span></span>

```console
> mlnet auto-train --task binary-classification --dataset "customer-feedback.tsv" --label-column-name Sentiment
```

![이미지](media/automate-training-with-cli/cli-model-generation.gif)

<span data-ttu-id="11cee-121">*Windows PowerShell*, \*macOS/Linux bash 또는 *Windows CMD*에서와 같은 방식으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-121">You can run it the same way on *Windows PowerShell*, \*macOS/Linux bash, or *Windows CMD*.</span></span> <span data-ttu-id="11cee-122">그러나 테이블 형식 자동 완성(매개 변수 제안)은 *Windows CMD*에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-122">However, tabular auto-completion (parameter suggestions) won't work on *Windows CMD*.</span></span>

## <a name="output-assets-generated"></a><span data-ttu-id="11cee-123">생성된 출력 자산</span><span class="sxs-lookup"><span data-stu-id="11cee-123">Output assets generated</span></span>

<span data-ttu-id="11cee-124">CLI `auto-train` 명령은 출력 폴더에 다음 자산을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-124">The CLI `auto-train` command generates the following assets in the output folder:</span></span>

- <span data-ttu-id="11cee-125">예측 실행에 사용할 수 있는 직렬화된 모델.zip("최상의 모델")</span><span class="sxs-lookup"><span data-stu-id="11cee-125">A serialized model .zip ("best model") ready to use for running predictions.</span></span> 
- <span data-ttu-id="11cee-126">다음을 포함한 C# 솔루션:</span><span class="sxs-lookup"><span data-stu-id="11cee-126">C# solution with:</span></span>
    - <span data-ttu-id="11cee-127">생성된 모델을 실행/채점하는 C# 코드(해당 모델의 최종 사용자 앱에서 예측 수행)</span><span class="sxs-lookup"><span data-stu-id="11cee-127">C# code to run/score that generated model (to make predictions in your end-user apps with that model).</span></span>
    - <span data-ttu-id="11cee-128">해당 모델을 생성하는 데 사용된 학습 코드를 포함한 C# 코드(교육용 또는 모델 재교육용)</span><span class="sxs-lookup"><span data-stu-id="11cee-128">C# code with the training code used to generate that model (for learning purposes or model retraining).</span></span>
- <span data-ttu-id="11cee-129">상세 구성/파이프라인을 포함하여 평가된 여러 알고리즘 전체의 모든 반복/스윕 정보가 담긴 로그 파일</span><span class="sxs-lookup"><span data-stu-id="11cee-129">Log file with information of all iterations/sweeps across the multiple algorithms evaluated, including their detailed configuration/pipeline.</span></span>

<span data-ttu-id="11cee-130">처음 두 자산은 생성된 ML 모델로 예측하기 위해 최종 사용자 앱(ASP.NET Core 웹앱, 서비스, 데스크톱 앱 등)에서 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-130">The first two assets can directly be used in your end-user apps (ASP.NET Core web app, services, desktop app, etc.) to make predictions with that generated ML model.</span></span>

<span data-ttu-id="11cee-131">세 번째 자산인 학습 코드는 생성된 모델을 학습하기 위해 CLI에서 사용한 ML.NET API 코드를 보여주므로, 바탕의 CLI 및 AutoML에서 선택한 특정 트레이너/알고리즘 및 하이퍼 매개 변수를 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-131">The third asset, the training code, shows you what ML.NET API code was used by the CLI to train the generated model, so you can retrain your model and investigate and iterate on which specific trainer/algorithm and hyperparameters were selected by the CLI and AutoML under the covers.</span></span> 

## <a name="understanding-the-quality-of-the-model"></a><span data-ttu-id="11cee-132">모델의 품질 이해</span><span class="sxs-lookup"><span data-stu-id="11cee-132">Understanding the quality of the model</span></span>

<span data-ttu-id="11cee-133">CLI 도구를 사용하여 “최상의 모델”을 생성할 때는 대상으로 하는 ML 작업에 적합하게 품질 메트릭(예: 정확도, R 제곱)이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-133">When you generate a 'best model' with the CLI tool, you see quality metrics (such as accuracy, and R-Squared) as appropriate for the ML task you are targeting.</span></span>

<span data-ttu-id="11cee-134">여기에서는 ML 작업에 따라 메트릭을 그룹화하여 요약하므로 자동 생성된 ‘최상의 모델’ 품질을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-134">Here we summarize those metrics grouped by ML task so you can understand the quality of your auto-generated 'best model'.</span></span>

### <a name="metrics-for-binary-classification-models"></a><span data-ttu-id="11cee-135">이진 분류 모델에 대한 메트릭</span><span class="sxs-lookup"><span data-stu-id="11cee-135">Metrics for Binary Classification models</span></span>

 <span data-ttu-id="11cee-136">다음은 CLI에서 찾은 상위 5개 모델에 대한 이진 분류 ML 작업 메트릭 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-136">The following displays the binary classification ML task metrics list for the top five models found by the CLI:</span></span> 

![이미지](media/automate-training-with-cli/cli-binary-classification-metrics.png)

<span data-ttu-id="11cee-138">정확도는 분류 문제에 대해 널리 사용되는 메트릭이나, 아래 참조에서 설명된 것처럼 최상의 모델을 선택하기 위해 항상 가장 적합한 메트릭인 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-138">Accuracy is a popular metric for classification problems, however accuracy is not always the best metric to select the best model from as explained in the references below.</span></span> <span data-ttu-id="11cee-139">추가적인 메트릭을 사용하여 모델 품질을 평가해야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-139">There are cases where you need to evaluate the quality of your model with additional metrics.</span></span>

<span data-ttu-id="11cee-140">CLI에서 출력하는 메트릭을 살펴보고 이해하려면 [이진 분류에 대한 메트릭](resources/metrics.md#metrics-for-binary-classification)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11cee-140">To explore and understand the metrics that are output by the CLI, see [Metrics for binary classification](resources/metrics.md#metrics-for-binary-classification).</span></span>

### <a name="metrics-for-multi-class-classification-models"></a><span data-ttu-id="11cee-141">다중 클래스 분류 모델에 대한 메트릭</span><span class="sxs-lookup"><span data-stu-id="11cee-141">Metrics for Multi-class Classification models</span></span>

 <span data-ttu-id="11cee-142">다음은 CLI에서 찾은 상위 5개 모델에 대한 다중 클래스 분류 ML 작업 메트릭 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-142">The following displays the multi-class classification ML task metrics list for the top five models found by the CLI:</span></span> 

![이미지](media/automate-training-with-cli/cli-multiclass-classification-metrics.png)

<span data-ttu-id="11cee-144">CLI에서 출력하는 메트릭을 살펴보고 이해하려면 [다중 클래스 분류에 대한 메트릭](resources/metrics.md#metrics-for-multi-class-classification)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11cee-144">To explore and understand the metrics that are output by the CLI, see [Metrics for multiclass classification](resources/metrics.md#metrics-for-multi-class-classification).</span></span>

### <a name="metrics-for-regression-models"></a><span data-ttu-id="11cee-145">회귀 모델에 대한 메트릭</span><span class="sxs-lookup"><span data-stu-id="11cee-145">Metrics for Regression models</span></span>

<span data-ttu-id="11cee-146">관찰된 값과 모델의 예측된 값 사이의 차이가 적고 편향되지 않은 경우 회귀 모델이 데이터에 잘 맞습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-146">A regression model fits the data well if the differences between the observed values and the model's predicted values are small and unbiased.</span></span> <span data-ttu-id="11cee-147">회귀는 특정 메트릭으로 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-147">Regression can be evaluated with certain metrics.</span></span>

<span data-ttu-id="11cee-148">CLI에서 찾은 상위 5개 품질 모델에 대해서도 비슷한 메트릭 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-148">You will see a similar list of metrics for the best top five quality models found by the CLI.</span></span> <span data-ttu-id="11cee-149">이 특정 사례는 회귀 ML 작업과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cee-149">In this particular case related to a regression ML task:</span></span>

![이미지](media/automate-training-with-cli/cli-regression-metrics.png)

<span data-ttu-id="11cee-151">CLI에서 출력하는 메트릭을 살펴보고 이해하려면 [회귀에 대한 메트릭](resources/metrics.md#metrics-for-regression)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11cee-151">To explore and understand the metrics that are output by the CLI, see [Metrics for regression](resources/metrics.md#metrics-for-regression).</span></span>

## <a name="see-also"></a><span data-ttu-id="11cee-152">참고 항목</span><span class="sxs-lookup"><span data-stu-id="11cee-152">See also</span></span>

- [<span data-ttu-id="11cee-153">ML.NET CLI 도구를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="11cee-153">How to install the ML.NET CLI tool</span></span>](how-to-guides/install-ml-net-cli.md)
- [<span data-ttu-id="11cee-154">자습서: ML.NET CLI를 사용한 이진 분류자 자동 생성</span><span class="sxs-lookup"><span data-stu-id="11cee-154">Tutorial: Auto generate a binary classifier using the ML.NET CLI</span></span>](tutorials/mlnet-cli.md)
- [<span data-ttu-id="11cee-155">ML.NET CLI 명령 참조</span><span class="sxs-lookup"><span data-stu-id="11cee-155">ML.NET CLI command reference</span></span>](reference/ml-net-cli-reference.md)
- [<span data-ttu-id="11cee-156">ML.NET CLI의 원격 분석</span><span class="sxs-lookup"><span data-stu-id="11cee-156">Telemetry in ML.NET CLI</span></span>](resources/ml-net-cli-telemetry.md)