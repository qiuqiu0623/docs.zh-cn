---
title: 计算指标以评估机器学习模型质量
description: 了解如何使用 ML.NET 来计算用于评估和验证机器学习模型质量的指标
ms.date: 03/05/2019
ms.custom: mvc,how-to
ms.openlocfilehash: d6409307cd283ae67d7546c4dc6e19e6089a0766
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2020
ms.locfileid: "73975844"
---
# <a name="calculate-metrics-to-evaluate-machine-learning-model-quality"></a>计算指标以评估机器学习模型质量

> [!NOTE]
> 本主题引用 ML.NET（目前处于预览状态），且材料可能会更改。 有关详细信息，请访问 [ML.NET](https://dotnet.microsoft.com/apps/machinelearning-ai/ml-dotnet) 页。

此操作说明和相关示例目前使用的是 ML.NET 版本 0.10  。 有关详细信息，请参阅 [dotnet/machinelearning GitHub 存储库](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes)上的发行说明。

训练模型后如何评估质量？ 每个机器学习任务都会公开用于质量评估的指标。

可使用任务的相应“上下文”来评估模型，如以下示例所示：

```csharp
// Read the test dataset.
var testData = reader.Read(testDataPath);
// Calculate metrics of the model on the test data.
var metrics = mlContext.Regression.Evaluate(model.Transform(testData), label: "Target");
```
