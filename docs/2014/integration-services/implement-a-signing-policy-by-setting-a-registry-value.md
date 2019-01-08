---
title: Implementare criteri per le firme impostando un valore del Registro di sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing policies [Integration Services]
ms.assetid: 64f6966f-2292-401f-acb1-2ccb5aee484a
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f8daa6582f18d9c5279e7539dd9c3740d90e36d2
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353205"
---
# <a name="implement-a-signing-policy-by-setting-a-registry-value"></a>Implementazione di criteri per le firme impostando un valore del Registro di sistema
  È possibile utilizzare un valore facoltativo del Registro di sistema per gestire i criteri dell'organizzazione per il caricamento dei pacchetti firmati o non firmati. Se si utilizza questo valore del Registro di sistema, è necessario crearlo in ogni computer in cui verranno eseguiti i pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e in cui si desidera applicare i criteri. Dopo l'impostazione del valore del Registro di sistema, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] controllerà o verificherà le firme prima di caricare i pacchetti.  
  
 Nella procedura di questo argomento viene descritto come aggiungere il valore facoltativo DWORD `BlockedSignatureStates` alla chiave del Registro di sistema HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS. Il valore di dati di `BlockedSignatureStates` determina se un pacchetto deve essere bloccato se è dotato di firma non attendibile o non valida oppure non è firmato. In relazione allo stato delle firme utilizzate per firmare pacchetti, il valore del Registro di sistema `BlockedSignatureStates` utilizza le definizioni seguenti:  
  
-   Per *firma valida* si intende una firma che può essere letta.  
  
-   Per *firma non valida* si intende una firma il cui checksum decrittografato, ovvero l'hash unidirezionale del codice del pacchetto crittografato mediante una chiave privata, non corrisponde al checksum decrittografato calcolato nell'ambito del processo di caricamento dei pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
-   Per *firma attendibile* si intende una firma creata tramite un certificato digitale firmato da un'autorità di certificazione radice attendibile. Con questa impostazione non è necessario che il firmatario sia contenuto nell'elenco degli autori attendibili.  
  
-   Per *firma non attendibile* si intende una firma che non può essere verificata in riferimento al rilascio da parte di un'autorità di certificazione radice attendibile o una firma non corrente.  
  
 Nella tabella seguente sono elencati i valori validi dei dati DWORD e i criteri associati.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|0|Nessuna restrizione amministrativa.|  
|1|Blocco delle firme non valide.<br /><br /> Con questa impostazione non vengono bloccati i pacchetti non firmati.|  
|2|Blocco delle firme non valide e non attendibili.<br /><br /> Con questa impostazione non vengono bloccati i pacchetti non firmati, ma vengono bloccate le firme a generazione automatica.|  
|3|Blocco delle firme non valide e non attendibili e dei pacchetti non firmati<br /><br /> Con questa impostazione vengono bloccate anche le firme a generazione automatica.|  
  
> [!NOTE]  
>  L'impostazione consigliata per `BlockedSignatureStates` è 3. Questa impostazione garantisce la massima protezione da pacchetti non firmati o firme non valide o non attendibili, ma potrebbe non essere appropriata per tutte le circostanze. Per altre informazioni su come firmare elementi digitali, vedere l'argomento "[Introduzione alla firma di codice](https://go.microsoft.com/fwlink/?LinkId=51414)" in MSDN Library.  
  
### <a name="to-implement-a-signing-policy-for-packages"></a>Per implementare criteri per le firme per i pacchetti  
  
1.  Fare clic sul menu **Start** e scegliere **Esegui**.  
  
2.  Nella finestra di dialogo Esegui, digitare `Regedit`, quindi fare clic su **OK**.  
  
3.  Individuare la chiave del Registro di sistema: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS  
  
4.  Fare clic con il pulsante destro del mouse su **MSDTS**, scegliere **Nuovo**e quindi **Valore DWORD**.  
  
5.  Aggiornare il nome del nuovo valore impostandolo su `BlockedSignatureStates`.  
  
6.  Fare doppio clic su `BlockedSignatureStates` e fare clic su **Modify**.  
  
7.  Nella finestra di dialogo **Modifica valore DWORD** digitare il valore 0, 1, 2 o 3.  
  
8.  Fare clic su **OK**.  
  
9. Scegliere **Esci** dal menu **File**.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica della sicurezza &#40;Integration Services&#41;](security/security-overview-integration-services.md)   
 [Identificazione dell'origine dei pacchetti con firme digitali](security/identify-the-source-of-packages-with-digital-signatures.md)  
  
  
