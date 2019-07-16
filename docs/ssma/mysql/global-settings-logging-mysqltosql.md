---
title: Impostazioni globali (registrazione) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0d033492-5ec3-473a-8de1-821894ec9518
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3d5188d701cd7930ff93c37aab74e11bba949d9b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896389"
---
# <a name="global-settings-logging--mysqltosql"></a>Impostazioni globali (registrazione) (MySQLToSQL)
Usare la **Global Settings** finestra di dialogo per specificare le impostazioni di registrazione per SSMA. In genere, è necessario modificare queste impostazioni solo quando si lavora con il supporto tecnico.  
  
Per accedere a questa finestra di dialogo, scegliere il **degli strumenti** dal menu **impostazioni globali** e quindi fare clic sul **registrazione** nella parte inferiore del riquadro di sinistra.  
  
## <a name="options"></a>Opzioni  
**A livello di messaggi**  
Le opzioni seguenti sono disponibili nella **a livello di messaggi**:  
  
|Opzione|Descrizione|  
|----------|---------------|  
|**[tutte le categorie]**|Utilizzato per impostare il livello di registrazione per tutte le opzioni seguenti.|  
|**Agente di raccolta dati**|Raccoglie i metadati relativi a schema di origine e lo salva il progetto.|  
|**Convertitore di tipi**|Converte le strutture degli oggetti di database di origine, ad esempio tabelle e stored procedure, nella corrispondente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] strutture.|  
|**Migrazione dei dati**|Esegue la migrazione di dati dal database di origine in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Formattatore**|Componente secondario del convertitore che consente di generare script per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dello schema.|  
|**Interfaccia utente grafica**|Messaggi che vengono visualizzati quando si usa lo strumento SSMA.|  
|**Linker**|Risolve gli identificatori SQL e vengono fornite informazioni ad altri componenti.|  
|**Altro**|Tutti i messaggi che non sono in nessun'altra categoria.|  
|**Parser**|Analizza lo schema di origine.|  
|**Synchronizer**|Oggetti di database in origine carichi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**TreeConverter**|Converte gli oggetti nei metadati di origine in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei metadati.|  
  
Per ogni opzione sotto **a livello di messaggi**, configurare uno dei seguenti livelli di registrazione per SSMA:  
  
|||  
|-|-|  
|**Errore irreversibile**|Scrivere solo i messaggi di errore irreversibile nel log.|  
|**Errore**|Scrivere nel registro errori e messaggi di errore irreversibile.|  
|**Avviso**|Scrittura avviso, errore e messaggi di errore irreversibile per il log.|  
|**info**|Scrivere nel log informativo, avviso, errore e messaggi di errore irreversibile.|  
|**Debug**|Scrivere tutti i messaggi, compresi i messaggi, nel log di debug.|  
  
**Percorso File di log**  
Il percorso del file e il nome dei file di log SSMA. Per specificare un nome diverso, scegliere il percorso corrente e quindi fare clic su Sfoglia ( **...** ) pulsante.  
  
**Dimensioni File di log**  
Le dimensioni massime del file di log in KB. La dimensione minima è 10 KB. La dimensione predefinito è 10240 KB.  
  
**Numero totale di file di log**  
Quando un log si riempie, SSMA verrà rinominare il file di log e avviarne uno nuovo. Con questa impostazione, specificare il numero massimo di file di log da mantenere. Il valore minimo è 2.  
  
