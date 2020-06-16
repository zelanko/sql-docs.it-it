---
title: Emulazione di variabili del pacchetto Oracle
description: Viene descritto il modo in cui SQL Server Migration Assistant (SSMA) per Oracle emula le variabili del pacchetto Oracle nel SQL Server.
author: nahk-ivanov
ms.prod: sql
ms.technology: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: ab7de81e16d1324aabd5f07421c1db4c51b3cf7c
ms.sourcegitcommit: e572f1642f588b8c4c75bc9ea6adf4ccd48a353b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2020
ms.locfileid: "84779463"
---
# <a name="emulating-oracle-package-variables"></a>Emulazione di variabili del pacchetto Oracle

Oracle supporta l'incapsulamento di variabili, tipi, stored procedure e funzioni in un pacchetto. Quando si convertono i pacchetti Oracle, è necessario convertire:

* Procedure e funzioni, sia pubbliche che private
* Variabili
* Cursori
* Routine di inizializzazione

Questo articolo descrive il modo in cui SQL Server Migration Assistant (SSMA) per Oracle converte le variabili di pacchetto in SQL Server.

## <a name="conversion-basics"></a>Nozioni fondamentali sulla conversione

Per archiviare le variabili del pacchetto, SSMA per Oracle utilizza stored procedure che si trovano in uno `ssma_oracle` schema speciale insieme alla `ssma_oracle.db_storage` tabella. Questa tabella è filtrata in base a `SPID` (identificatore di sessione) e ora di accesso. Questo filtro consente di distinguere le variabili di diverse sessioni.

All'inizio di ogni procedura del pacchetto convertito SSMA viene eseguita una chiamata alla `ssma_oracle.db_check_init_package` procedura speciale, che controlla se il pacchetto è inizializzato e lo Inizializza se necessario. Ogni procedura di inizializzazione pulisce la tabella di archiviazione e imposta i valori predefiniti per ogni variabile del pacchetto.

## <a name="example"></a>Esempio

Si consideri l'esempio seguente per la conversione di diverse variabili del pacchetto:

```sql
CREATE OR REPLACE PACKAGE MY_PACKAGE
IS
    space varchar(1) := ' ';
    unitname varchar(128) := 'My Simple Package';
    ts date := sysdate;
END;
```

SSMA lo converte nel seguente codice Transact-SQL:

```sql
CREATE PROCEDURE dbo.MY_PACKAGE$SSMA_Initialize_Package
AS
BEGIN
    EXECUTE ssma_oracle.db_clean_storage

    EXECUTE ssma_oracle.set_pv_varchar
        DB_NAME(),
        'DBO',
        'MY_PACKAGE',
        'SPACE',
        ' '

    EXECUTE ssma_oracle.set_pv_varchar
        DB_NAME(),
        'DBO',
        'MY_PACKAGE',
        'UNITNAME',
        'My Simple Package'

    DECLARE
        @temp datetime2

    SET @temp = sysdatetime()

    EXECUTE sysdb.ssma_oracle.set_pv_datetime2
      DB_NAME(),
      'DBO',
      'MY_PACKAGE',
      'TS',
      @temp
END
```

## <a name="emulating-get-and-set-methods-for-package-variables"></a>Emulazione di metodi get e set per le variabili del pacchetto

Oracle USA `Get` `Set` i metodi e per le variabili del pacchetto, per evitare che altri sottoprogrammi leggano e li scrivano direttamente. Se è necessario lasciare disponibili alcune variabili tra le chiamate al sottoprogramma nella stessa sessione, queste variabili vengono considerate come variabili globali.

Per ovviare a questa regola di ambito, SSMA per Oracle USA stored procedure come `ssma_oracle.set_pv_varchar` per ogni tipo di variabile. Per accedere a queste variabili, SSMA utilizza un set di `get_*` `set_*` routine e funzioni indipendenti dalla transazione.

| Tipo di dati in Oracle | `Set`Procedura SSMA           |
| ------------------- | ------------------------------ |
| VARCHAR             | `ssma_oracle.set_pv_varchar`   |
| DATE                | `ssma_oracle.set_pv_datetime2` |
| CHAR                | `ssma_oracle.set_pv_varchar`   |
| INT                 | `ssma_oracle.set_pv_float`     |
| FLOAT               | `ssma_oracle.set_pv_float`     |

Per distinguere le variabili da diverse sessioni, SSMA archivia le variabili insieme ai relativi `SPID` (identificatore di sessione) e all'ora di accesso della sessione. Pertanto `get_*` , le `set_*` routine e mantengono le variabili indipendenti dalle sessioni che li eseguono.
