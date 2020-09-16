---
description: Finestra di dialogo Indice full-text (Visual Database Tools)
title: Finestra di dialogo Indice full-text
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextindex
ms.assetid: ef45b585-2567-4abe-b421-9fd0994e0146
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 566239ac238afb66650c50cd9d96c8fa81d3f70c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497144"
---
# <a name="full-text-index-dialog-box-visual-database-tools"></a>Finestra di dialogo Indice full-text (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Questa finestra di dialogo consente di creare un indice full-text per eseguire ricerche full-text nelle colonne basate su testo delle tabelle di database. Poiché un indice di questo tipo si basa su un indice normale, è necessario innanzitutto creare tale indice. L'indice normale deve essere creato utilizzando una sola colonna non Null, preferibilmente con valori non particolarmente elevati.  
  
> [!NOTE]
> Per creare un indice full-text, è innanzitutto necessario creare un catalogo full-text per il database utilizzando uno strumento esterno quale [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o Enterprise Manager.  
> 
> [!NOTE]
> La funzionalità degli indici full-text non è disponibile in tutte le edizioni di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2012](https://msdn.microsoft.com/5da61ff5-12b9-48e6-b3c8-0dacca1751c4).  
  
## <a name="options"></a>Opzioni  
**Indice full-text selezionato**  
Elenca gli indici full-text disponibili. Selezionarne uno per visualizzarne le proprietà nella griglia a destra. Se l'elenco è vuoto, significa che per la tabella non sono state definite relazioni full-text.  
  
**Aggiungere**  
Crea un nuovo indice full-text.  
  
**Elimina**  
Elimina l'elemento selezionato nell'elenco **Indice full-text selezionato** .  
  
**Categoria Generale**  
Se viene espansa, visualizza **Colonne** e **Nome catalogo full-text**.  
  
**Colonne**  
Visualizza un elenco separato da virgole con i nomi delle colonne in cui è possibile effettuare la ricerca full-text. Per visualizzare l'elenco completo, fare clic sul pulsante con i puntini di sospensione ( **...** ) a sinistra del campo della proprietà.  
  
**Full-Text Catalog Name**  
Visualizza il nome del catalogo full-text in cui è archiviato l'indice full-text. Per archiviare l'indice in un catalogo diverso, fare clic sul nome del catalogo e selezionarne un altro dall'elenco a discesa.  
  
> [!NOTE]  
> Il catalogo deve essere già stato creato con uno strumento esterno, ad esempio [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o Enterprise Manager.  
  
**Categoria Identità**  
Se viene espansa, visualizza il campo del nome dell'indice.  
  
**Nome**  
Visualizza il nome specificato dal sistema per l'indice full-text.  
  
**Categoria Progettazione tabelle**  
Se viene espansa, visualizza le proprietà che determinano il funzionamento dell'indice.  
  
**Attivo**  
Indica se è possibile eseguire una ricerca full-text utilizzando l'indice full-text.  
  
**Impostazione ricerca delle modifiche**  
Visualizza lo stato della ricerca delle modifiche per l'indice: Manuale, Automatico o Disattivato.  
  
**Ricerca completata**  
Indica se la ricerca più recente è stata completata. Se la proprietà è impostata su No, è in corso una ricerca.  
  
**Data e ora di fine ricerca corrente o più recente**  
Visualizza la data e l'ora in cui è terminata la ricerca più recente.  
  
**Errori nella ricerca corrente o più recente**  
Visualizza il numero di errori verificatisi nella ricerca corrente o più recente.  
  
**Versione indice**  
Visualizza la versione dello schema della tabella al momento in cui è stata avviata la ricerca.  
  
**Righe nella ricerca corrente o più recente**  
Visualizza il numero di righe aggiornate nella ricerca corrente o più recente.  
  
**Data e ora di inizio ricerca corrente o più recente**  
Visualizza la data e l'ora in cui è iniziata la ricerca corrente o più recente.  
  
**Timestamp per ricerca successiva**  
Visualizza la data e l'ora di inizio della prossima ricerca.  
  
**Tipo di ricerca corrente o più recente**  
Visualizza il tipo della ricerca corrente o più recente: Completa, Incrementale, Aggiornamento o Propagazione automatica.  
  
**Nome indice univoco**  
Visualizza un elenco di tutti i nomi delle colonne del database con indici di colonne singole univoci. Queste colonne possono essere utilizzate per creare un indice full-text.  
  
## <a name="see-also"></a>Vedere anche  
[Utilizzare l'Indicizzazione guidata full-text](https://msdn.microsoft.com/3e9d9605-6525-4781-9168-fdaa06db3459)  
[CREATE FULLTEXT INDEX (Transact-SQL)](https://msdn.microsoft.com/8b80390f-5f8b-4e66-9bcc-cabd653c19fd)  
  
