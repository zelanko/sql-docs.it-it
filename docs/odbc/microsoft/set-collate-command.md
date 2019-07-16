---
title: SET COLLATE (comando) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a7701edd4c1902399f1d040ae9027365bdf04ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997747"
---
# <a name="set-collate-command"></a>SET COLLATE (comando)
Specifica una sequenza di confronto per i campi di caratteri nelle operazioni di ordinamento e indicizzazione successive.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>Argomenti  
 *cSequenceName*  
 Specifica una sequenza di confronto. Nella tabella seguente sono descritte le opzioni di sequenza di regole di confronto disponibili.  
  
|Opzioni|Linguaggio|  
|-------------|--------------|  
|OLANDESE|Olandese|  
|GENERAL|Inglese, francese, tedesco, spagnolo moderno, portoghese e altre lingue dell'Europa occidentale|  
|TEDESCO|Ordine della Rubrica telefonica tedesco (DIN)|  
|ISLANDA|Islandese|  
|COMPUTER|Computer (la sequenza di confronto predefinite per le versioni precedenti di FoxPro)|  
|NORDAN|Norvegese, danese|  
|SPAGNOLO|Spagnolo tradizionale|  
|SWEFIN|Svedese, finlandese|  
|UNIQWT|Peso univoco|  
  
> [!NOTE]  
>  Quando si specifica l'opzione spagnolo *ch* è una singola lettera che ordina tra *c* e *1!d*, e *ll* Ordina tra  *l* e *m*.  
  
 Se si specifica un'opzione della sequenza delle regole di confronto come una stringa di caratteri letterali, assicurarsi di racchiuderlo tra virgolette l'opzione:  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 MACCHINA è l'opzione della sequenza delle regole di confronto predefinito e si che hanno familiari con gli utenti di Xbase sequenza. Caratteri vengono ordinati come appaiono nella tabella codici corrente.  
  
 GENERALE può essere preferibile per gli utenti degli Stati Uniti ed Europa occidentale. Caratteri vengono ordinati come appaiono nella tabella codici corrente. Nelle versioni di FoxPro precedenti alla 2.5, gli indici potrebbero essere stati creati usando il **superiore**() o **inferiore**funzioni () per convertire i campi di tipo carattere in un caso coerente. Nelle versioni di FoxPro entro 2.5, è possibile specificare l'opzione della sequenza delle regole di confronto generali e omettere il **superiore**conversione ().  
  
 Se si specifica un'opzione della sequenza delle regole di confronto diverse da computer e se si crea un file IDX, viene sempre creato un IDX compact.  
  
 Usare SET("COLLATE") per restituire la sequenza di confronto correnti.  
  
 È possibile specificare una sequenza di confronto per un'origine dati usando il [la finestra di dialogo di ODBC Visual FoxPro Setup](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) oppure usando la parola chiave Collate nella stringa di connessione con [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md). Questa impostazione equivale a eseguire il comando seguente:  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>Note  
 SET COLLATE consente di tabelle degli ordini che contiene i caratteri accentati per qualsiasi delle lingue supportate. Modifica dell'impostazione di SET COLLATE non influisce sulla sequenza di ordinamento di indici già aperti. Visual FoxPro gestisce automaticamente gli indici esistenti, offrendo la flessibilità necessaria per creare molti tipi diversi di indici, anche per lo stesso campo.  
  
 Ad esempio, se viene creato un indice con SET COLLATE impostato su Generale e l'impostazione SET COLLATE in un secondo momento viene modificato in spagnolo, l'indice viene mantenuta la sequenza di confronto generali.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo di configurazione ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
