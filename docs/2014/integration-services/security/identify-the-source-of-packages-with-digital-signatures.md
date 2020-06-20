---
title: Identificare l'origine dei pacchetti con firme digitali | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing packages [Integration Services]
- certificates [Integration Services]
- packages [Integration Services], security
- security [Integration Services], certificates
- signing policies [Integration Services]
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 269aef896c485f0a383a35eae6d750e939868c29
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84963846"
---
# <a name="identify-the-source-of-packages-with-digital-signatures"></a>Identificazione dell'origine dei pacchetti con firme digitali
  Un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] può essere firmato con un certificato digitale per identificarne l'origine. Dopo la firma di un pacchetto con un certificato digitale, è possibile configurare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per controllare o verificare la firma digitale prima del caricamento del pacchetto. Per fare in modo che [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] controlli la firma, impostare un'opzione in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o nell'utilità **dtexec** (dtexec.exe) oppure impostare un valore facoltativo del Registro di sistema.  
  
## <a name="signing-a-package-with-a-digital-certificate"></a>Firma di un pacchetto con un certificato digitale  
 Prima di poter firmare un pacchetto con un certificato digitale, è necessario ottenere o creare il certificato. Dopo aver ottenuto il certificato, è possibile utilizzarlo per la firma del pacchetto. Per altre informazioni su come ottenere un certificato e usarlo per firmare un pacchetto, vedere [Firmare un pacchetto con un certificato digitale](../sign-a-package-by-using-a-digital-certificate.md).  
  
## <a name="setting-an-option-to-check-the-package-signature"></a>Impostazione di un'opzione per la verifica della firma del pacchetto  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e l'utilità **dtexec** includono un'opzione per configurare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per la verifica della firma digitale dei pacchetti firmati. È possibile usare [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o l'utilità **dtexec** a seconda che si voglia controllare tutti i pacchetti o solo alcuni pacchetti specifici:  
  
-   Per controllare la firma digitale di tutti i pacchetti prima del caricamento in fase di progettazione, impostare l'opzione **Controlla firma digitale al caricamento di un pacchetto** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Questa opzione è un'impostazione globale per tutti i pacchetti di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Per ulteriori informazioni, vedere [General Page](../general-page-of-integration-services-designers-options.md).  
  
-   Per controllare la firma digitale di un singolo pacchetto, specificare l' `/VerifyS[igned]` opzione quando si usa l'utilità **dtexec** per eseguire il pacchetto. Per altre informazioni, vedere [dtexec Utility](../packages/dtexec-utility.md).  
  
## <a name="setting-a-registry-value-to-check-the-package-signature"></a>Impostazione di un valore del Registro di sistema per la verifica della firma del pacchetto  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]supporta anche un valore facoltativo del registro di sistema, **BlockedSignatureStates**, che è possibile usare per gestire i criteri di un'organizzazione per il caricamento di pacchetti firmati e non firmati. Il valore del Registro di sistema consente di impedire il caricamento di pacchetti non firmati o con firme non valide o non attendibili. Per altre informazioni su come impostare questo valore del Registro di sistema, vedere [Implementare criteri per le firme tramite l'impostazione di un valore del Registro di sistema](../implement-a-signing-policy-by-setting-a-registry-value.md).  
  
> [!NOTE]  
>  Il valore facoltativo **BlockedSignatureStates** del registro di sistema può specificare un'impostazione più restrittiva rispetto all'opzione per la firma digitale impostata in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o alla riga di comando **dtexec** . In questo caso, l'impostazione del Registro di sistema più restrittiva ha la precedenza rispetto ad altre impostazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services &#40;pacchetti&#41; SSIS](../integration-services-ssis-packages.md)   
 [Panoramica sulla sicurezza &#40;Integration Services&#41;](security-overview-integration-services.md)  
  
  
