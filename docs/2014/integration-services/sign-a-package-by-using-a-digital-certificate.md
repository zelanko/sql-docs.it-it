---
title: Firmare un pacchetto tramite certificato digitale | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- digital signatures [Integration Services]
- signing packages [Integration Services]
- signatures [Integration Services]
ms.assetid: 182b115e-0fe2-4717-8dff-183f9eb6e397
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 31da686dbf25922205ea4d1b03ecaa3758457573
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055620"
---
# <a name="sign-a-package-by-using-a-digital-certificate"></a>Firma di un pacchetto tramite certificato digitale
  Questo argomento illustra come firmare un pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] con un certificato digitale. È possibile utilizzare una firma digitale, insieme ad altre impostazioni, per evitare il caricamento e l'esecuzione di pacchetti non validi.  
  
 Prima di poter firmare un pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , è necessario effettuare le attività seguenti:  
  
-   Creare o ottenere una chiave privata da associare al certificato e archiviarla nel computer locale.  
  
-   Ottenere un certificato a scopo di firma del codice da un'autorità di certificazione attendibile. Per ottenere o creare un certificato, è possibile utilizzare uno dei metodi seguenti:  
  
    -   Ottenere un certificato da un'autorità di certificazione commerciale pubblica che emette certificati.  
  
    -   Ottenere un certificato da un server dei certificati che consente alle organizzazioni di emettere certificati internamente. È necessario aggiungere il certificato radice usato per firmare il certificato nell'archivio **Autorità di certificazione radice disponibili nell'elenco locale** . Per aggiungere il certificato radice, è possibile utilizzare lo snap-in Certificati per [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console (MMC). Per altre informazioni, vedere l'argomento "[Certificate Services](https://go.microsoft.com/fwlink/?LinkId=100755)" (Servizi certificati) in MSDN Library.  
  
    -   Creare un certificato solo a scopo di testing. Lo strumento di creazione certificati (Makecert.exe) genera certificati X.509 solo a scopo di testing. Per altre informazioni, vedere l'argomento "[Strumento di creazione certificati (Makecert.exe)](https://go.microsoft.com/fwlink/?LinkId=100756)" in MSDN Library.  
  
     Per ulteriori informazioni sui certificati, vedere la Guida relativa allo snap-in Certificati. Per altre informazioni sulla firma di risorse digitali, vedere l'argomento "[Signing and Checking Code with Authenticode](https://go.microsoft.com/fwlink/?LinkId=78100)" (Firma e verifica del codice con Authenticode) in MSDN Library.  
  
-   Verificare che il certificato sia stato abilitato per la firma di codice. Per determinare se un certificato è abilitato per la firma di codice, controllare le proprietà del certificato nello snap-in Certificati.  
  
-   Archiviare il certificato nell'archivio personale.  
  
 Dopo avere completato le attività precedenti, è possibile utilizzare la procedura descritta di seguito per firmare un pacchetto.  
  
### <a name="to-sign-a-package"></a>Per firmare un pacchetto  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto da firmare.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] scegliere **Firma digitale** dl menu **SSIS**.  
  
4.  Nella finestra di dialogo **Firma digitale** fare clic su **Firma**.  
  
5.  Nella finestra di dialogo **Seleziona certificato** selezionare un certificato.  
  
6.  (Facoltativo) Fare clic su **Visualizza certificato**per visualizzare informazioni sul certificato.  
  
7.  Fare clic su **OK** per chiudere la finestra di dialogo **Seleziona certificato** .  
  
8.  Fare clic su **OK** per chiudere la finestra di dialogo **Firma digitale** .  
  
9. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
     Anche se il pacchetto è stato firmato, è necessario configurare [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per controllare o verificare la firma digitale prima del caricamento del pacchetto. Per altre informazioni, vedere [Identificazione dell'origine dei pacchetti con firme digitali](security/identify-the-source-of-packages-with-digital-signatures.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica sulla sicurezza &#40;Integration Services&#41;](security/security-overview-integration-services.md)  
  
  
