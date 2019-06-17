---
title: Impostazioni globali (registrazione) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d314a2ca-ea2e-46e0-ae5e-8774841da91b
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7d632b040a5124d73470ce825af91e254866a0ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299222"
---
# <a name="global-settings-logging-db2tosql"></a>Impostazioni globali (registrazione) (DB2ToSQL)
Usare la **Global Settings** finestra di dialogo per specificare le impostazioni di registrazione per SSMA. In genere, è necessario modificare queste impostazioni solo quando si lavora con il supporto tecnico.  
  
Per accedere a questa finestra di dialogo, scegliere il **degli strumenti** dal menu **impostazioni globali** e quindi fare clic sul **registrazione** nella parte inferiore del riquadro di sinistra.  
  
## <a name="options"></a>Opzioni  
**A livello di messaggi**  
Le opzioni seguenti sono disponibili nella **a livello di messaggi**:  
  
|Opzione|Descrizione|  
|----------|---------------|  
|**[tutte le categorie]**|Utilizzato per impostare il livello di registrazione per tutte le opzioni seguenti.|  
|**Agente di raccolta dati**|Raccoglie i metadati relativi a schema di origine e lo salva il progetto.|  
|**Converter**|Converte le strutture degli oggetti di database di origine, ad esempio tabelle e stored procedure, nella corrispondente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] strutture.|  
|**Migrazione dei dati**|Esegue la migrazione di dati dal database di origine in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Formatter**|Componente secondario del convertitore che consente di generare script per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dello schema.|  
|**Interfaccia utente grafica**|Messaggi che vengono visualizzati quando si usa lo strumento SSMA.|  
|**Linker**|Risolve gli identificatori SQL e vengono fornite informazioni ad altri componenti.|  
|**Altro**|Tutti i messaggi che non sono in nessun'altra categoria.|  
|**Parser**|Analizza lo schema di origine.|  
|**Synchronizer**|Oggetti di database in origine carichi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**TreeConverter**|Converte gli oggetti nei metadati di origine in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei metadati.|  
|**Tester**|Messaggi che vengono visualizzati quando si usa il Tester di SSMA.|  
  
Per ogni opzione sotto **a livello di messaggi**, configurare uno dei seguenti livelli di registrazione per SSMA:  
  
|||  
|-|-|  
|**Errore irreversibile**|Scrivere solo i messaggi di errore irreversibile nel log.|  
|**Errore**|Scrivere nel registro errori e messaggi di errore irreversibile.|  
|**Avviso**|Scrittura avviso, errore e messaggi di errore irreversibile per il log.|  
|**info**|Scrivere nel log informativo, avviso, errore e messaggi di errore irreversibile.|  
|**Debug**|Scrivere tutti i messaggi, compresi i messaggi, nel log di debug.|  
  
**Percorso file di log**  
Il percorso del file e il nome dei file di log SSMA. Per specificare un nome diverso, scegliere il percorso corrente e quindi fare clic su Sfoglia ( **...** ) pulsante.  
  
**Dimensioni file di log**  
Le dimensioni massime del file di log in KB. La dimensione minima è 10 KB. La dimensione predefinito è 10240 KB.  
  
**Numero totale di file di log**  
Quando un log si riempie, SSMA verrà rinominare il file di log e avviarne uno nuovo. Con questa impostazione, specificare il numero massimo di file di log da mantenere. Il valore minimo è 2.  
  
