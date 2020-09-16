---
description: Informazioni sul blocco delle righe
title: Informazioni sul blocco delle righe | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 63c76a2f-f2b9-461f-8904-acbda0169ac3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69b04db86ce8784f5f346a4ac0d19b2bedd0e456
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488034"
---
# <a name="understanding-row-locking"></a>Informazioni sul blocco delle righe

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa blocchi di riga di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questi blocchi consentono di implementare i controlli della concorrenza tra più utenti che eseguono contemporaneamente modifiche in un database. Per impostazione predefinita, le transazioni e i blocchi sono gestiti a livello di singola connessione. Se, ad esempio, tramite un'applicazione vengono aperte due connessioni JDBC, i blocchi acquisiti da una connessione non possono essere condivisi con l'altra connessione. Nessuna delle due connessioni può acquisire blocchi che entrerebbero in conflitto con i blocchi mantenuti attivi dall'altra connessione.

> [!NOTE]  
> Se viene utilizzato il blocco di riga, tutte le righe nel buffer di recupero sono bloccate, pertanto un'impostazione molto grande per la dimensione di recupero può influire sulla concorrenza.

Il blocco viene utilizzato per garantire l'integrità delle transazioni e la coerenza dei database. Il blocco impedisce agli utenti di leggere dati di cui è in corso la modifica da parte di altri utenti e impedisce che gli stessi dati vengano modificati contemporaneamente da più utenti. Se il blocco non viene utilizzato, i dati inclusi in un database possono diventare incorretti a livello logico e le query eseguite su tali dati possono produrre risultati imprevisti.

> [!NOTE]  
> Per altre informazioni sul blocco di riga in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere "Uso dei blocchi in [!INCLUDE[ssDE](../../includes/ssde_md.md)]" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="see-also"></a>Vedere anche

[Gestione dei set di risultati con il driver JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)
