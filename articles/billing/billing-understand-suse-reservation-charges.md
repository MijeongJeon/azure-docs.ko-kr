---
title: SUSE 요금제 할인 및 사용량 이해 - Azure 예약 | Microsoft Docs
description: 가상 머신의 SUSE 소프트웨어에 SUSE 요금제 할인이 적용되는 방법을 알아봅니다.
services: billing
documentationcenter: ''
author: yashesvi
manager: yashar
editor: ''
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/28/2018
ms.author: banders
ms.openlocfilehash: a9f784d7e7ed21a5a10a2f5e16125d60e7b9667f
ms.sourcegitcommit: 5839af386c5a2ad46aaaeb90a13065ef94e61e74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2019
ms.locfileid: "57863477"
---
# <a name="understand-how-the-suse-linux-enterprise-software-plan-discount-is-applied"></a>SUSE Linux Enterprise 소프트웨어 요금제 할인이 적용되는 방식 이해

SUSE Linux 요금제를 구입한 후에 예약에 해당하는 배포된 SUSE VM(가상 머신)에 자동으로 할인이 적용됩니다. SUSE Linux 요금제는 Azure VM에서 SUSE 소프트웨어를 실행하는 비용을 포함합니다.

적절한 SUSE Linux 요금제를 구입하려면 실행하는 SUSE VM과 해당 VM에 있는 vCPU 수를 이해해야 합니다. 다음 섹션은 사용량 CSV 파일에서 구입할 요금제를 식별하는 데 도움이 됩니다.

## <a name="discount-applies-to-different-vm-sizes-with-instance-size-flexibility"></a>할인은 인스턴스 크기 유연성이 있는 다양한 VM 크기에 적용됩니다.

Reserved VM Instances와 같이 SUSE 요금제 구매는 인스턴스 크기 유연성을 제공합니다. 즉, 다른 vCPU 수를 사용하는 VM을 배포할 때도 할인이 적용됩니다. 소프트웨어 요금제 내의 다른 VM 크기에도 할인이 적용됩니다.

할인 금액은 다음 표에 나열된 비율에 따라 달라집니다. 이 비율은 해당 그룹의 각 미터법에 대한 상대적 공간을 비교합니다. 이 비율은 VM vCPU에 따라 달라집니다. SUSE Linux 요금제 할인을 받는 VM 인스턴스 수를 계산할 때 이 비율 값을 사용합니다.

예를 들어, 3~4개의 vCPU가 있는 VM에 대해 SUSE Linux Enterprise Server for HPC 우선 순위용 요금제를 구입하는 경우 해당 예약에 대한 비율은 2입니다. 이 할인은 다음에 대한 SUSE 소프트웨어 비용을 포함합니다.

- 1~2개의 vCPU가 있는 배포된 VM 2개
- 3~4개의 vCPU가 있는 배포된 VM 1개
- 또는 5개 이상의 vCPU가 있는 VM의 0.77 또는 약 77%

5개 이상의 vCPU에 대한 비율은 2.6입니다. 따라서 5개 이상의 vCPU가 있는 SUSE에 대한 예약은 소프트웨어 비용에서 약 77%에 해당하는 일부만 부과합니다.

## <a name="understand-your-suse-vm-usage-before-buying-a-suse-linux-plan"></a>SUSE Linux 요금제를 구입하기 전에 SUSE VM 사용량 이해

다음 표에는 예약을 구입할 수 있는 소프트웨어 요금제, 해당 관련 사용량 미터 및 각각의 비율이 나와 있습니다.

### <a name="suse-linux-enterprise-server-for-hpc-priority"></a>SUSE Linux Enterprise Server for HPC 우선 순위

Azure Portal Marketplace 이름:

- SLES 12 SP3 for HPC(우선 순위)

|SUSE VM | MeterId| 비율| 예제 VM 크기|
| -------| ------------------------| --- |--- |
|SLES for HPC 1-2 vCPU|e275a668-ce79-44e2-a659-f43443265e98|1|D2s_v3|
|SLES for HPC 3-4 vCPU|e531e1c0-09c9-4d83-b7d0-a2c6741faa22|2|D4s_v3|
|SLES for HPC 5+ vCPU|4edcd5a5-8510-49a8-a9fc-c9721f501913|2.6|D8s_v3|

### <a name="suse-linux-enterprise-server-for-hpc-standard"></a>SUSE Linux Enterprise Server for HPC Standard

Azure Portal Marketplace 이름:

- SLES 12 SP3 for HPC

|SUSE VM | MeterId | 비율|예제 VM 크기|
| ------- | --- | ------------------------| --- |
|SLES for HPC 1-2 vCPU |8c94ad45-b93b-4772-aab1-ff92fcec6610|1|D2s_v3|
|SLES for HPC 3-4 vCPU|4ed70d2d-e2bb-4dcd-b6fa-42da71861a1c|1.92308|D4s_v3|
|SLES for HPC 5+ vCPU |907a85de-024f-4dd6-969c-347d47a1bdff|2.92308|D8s_v3|

### <a name="suse-linux-enterprise-server-for-sap-priority"></a>SUSE Linux Enterprise Server for SAP 우선 순위

Azure Portal Marketplace 이름:

- SLES for SAP 15(우선 순위)
- SLES for SAP 12 SP3(우선 순위)
- SLES for SAP 12 SP2(우선 순위)

|SUSE VM | MeterId | 비율|예제 VM 크기|
| ------- |------------------------| --- | --- |
|SLES for SAP 우선 순위 1-2 vCPU|497fe0b6-fa3c-4e3d-a66b-836097244142|1|D2s_v3|
|SLES for SAP 우선 순위 3-4 vCPU |847887de-68ce-4adc-8a33-7a3f4133312f|2|D4s_v3|
|SLES for SAP 우선 순위 5+ vCPU |18ae79cd-dfce-48c9-897b-ebd3053c6058|2.41176|D8s_v3|

### <a name="suse-linux-enterprise-server-priority"></a>SUSE Linux Enterprise Server 우선 순위

Azure Portal Marketplace 이름:

- SLES 15(우선 순위)
- SLES 12 SP3(우선 순위)
- SLES 11 SP4(우선 순위)

|SUSE VM | MeterId | 비율|예제 VM 크기|
| ------- |------------------------| --- |--- |
|SLES 1 vCPU|462cd632-ec6b-4663-b79f-39715f4e8b38|1|B1ms|
|SLES 2-4 vCPU |924bee71-5eb8-424f-83ed-a58823c33908|2|D4s_v3|
|SLES 2-4 vCPU |60b3ae9d-e77a-46b2-9cdf-92fa87407969|2|D4s_v3|
|SLES 6 vCPU |e8862232-6131-4dbe-bde4-e2ae383afc6f|3||
|SLES 8 vCPU |e11331a8-fd32-4e71-b60e-4de2a818c67a|3.2|D8s_v3|
|SLES 12 코어 vCPU |a5afd00d-d3ef-4bcd-8b42-f158b2799782|3.2||
|SLES 16 vCPU |bb21066f-fe46-46d3-8006-b326b1663e52|3.2| D16s_v3|
|SLES 20 vCPU |c5228804-1de6-4bd4-a61c-501d9003acc8|3.2| |
|SLES 24 코어 vCPU |4075 ac11 822ccde9e8f6-005 d|3.2| ND24s|
|SLES 32 vCPU |180c1a0a-b0a5-4de3-a032-f92925a4bf90|3.2| D32s_v3|
|SLES 40 코어 vCPU |a161d3d3-0592-4956-9b64-6829678b6506|3.2||
|SLES 64 vCPU |7f5a36ed-d5b5-4732-b6bb-837dbf0fb9d8|3.2| D64s_v3|
|SLES 72 코어 vCPU |93329a72-24d7-4faa-93d9-203f367ed334|3.2|F72s_v2|
|SLES 96 코어 vCPU |2018c3a8-ff13-41f8-b64d-9558c5206547|3.2||
|SLES 128 코어 vCPU |ac27e4d7-44b5-4fee-bc1a-78ac5b4abaf7|3.2| M128ms|

### <a name="suse-linux-enterprise-server-standard"></a>SUSE Linux Enterprise Server Standard

Azure Portal Marketplace 이름:

- SLES 15
- SLES 15(표준)
- SLES 12 SP3(표준)

|SUSE VM | MeterId | 비율|예제 VM 크기|
| ------- |------------------------| --- |--- |
|SLES 1-2 코어 vCPU |4b2fecfc-b110-4312-8f9d-807db1cb79ae|1|D2s_v3|
|SLES 3-4 코어 vCPU |0c3ebb4c-db7d-4125-b45a-0534764d4bda|1.92308|D4s_v3|
|SLES 5+ vCPU |7b349b65-d906-42e5-833f-b2af38513468|2.30769| D8s_v3|

## <a name="next-steps"></a>다음 단계

예약에 대해 자세히 알아보려면 다음 문서를 참조하세요.

- [Azure 예약이란?](billing-save-compute-costs-reservations.md)
- [Azure 예약에서 SUSE 소프트웨어 요금제에 대한 선불](../virtual-machines/linux/prepay-suse-software-charges.md)
- [Azure Reserved VM Instances를 사용하여 Virtual Machines 선불 결제](../virtual-machines/windows/prepay-reserved-vm-instances.md)
- [Azure Reservations 관리](billing-manage-reserved-vm-instance.md)
- [종량제 구독의 예약 사용량 이해](billing-understand-reserved-instance-usage.md)
- [엔터프라이즈 등록에서 예약 사용량 이해](billing-understand-reserved-instance-usage-ea.md)

## <a name="need-help-contact-us"></a>도움 필요 시 문의하세요.

문의 사항이 있거나 도움이 필요한 경우 [지원 요청을 만드는](https://go.microsoft.com/fwlink/?linkid=2083458)합니다.