---
title: Script per la concessione di autorizzazioni per Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], script to grant permissions
ms.assetid: d742fd30-347a-452f-b5fc-b03232360c6b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d7c61a21f149a50c4893c9c82d3624e0905a481b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52778123"
---
# <a name="script-to-grant-oracle-permissions"></a>Script per la concessione di autorizzazioni per Oracle
  Lo script descritto in questo argomento viene utilizzato durante la configurazione di un database Oracle i cui i dati verranno pubblicati tramite la replica [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Questo script è disponibile anche nella directory seguente dopo l'installazione: *\<unità>*:\\\Programmi\Microsoft SQL Server\\*\<NomeIstanza>* \MSSQL\Install\oracleadmin.sql. Per altre informazioni sulla configurazione del database Oracle, vedere [Configurare un server di pubblicazione Oracle](configure-an-oracle-publisher.md).  
  
> [!NOTE]  
>  Nello script è inclusa l'istruzione `GRANT CREATE ANY TRIGGER TO &&AdminLogin;`, obbligatoria per i trigger utilizzati nella replica transazionale. Se si utilizza soltanto la replica snapshot, rimuovere questa riga dallo script.  
  
 **Per eseguire lo script dall'utilità Oracle SQL\*Plus**  
  
1.  Nel server di distribuzione SQL Server, aprire una finestra del prompt dei comandi.  
  
2.  Per utilizzare SQL*PLUS per la connessione al database Oracle ed eseguire lo script oracleadmin.sql dalla directory di installazione predefinita, digitare la sintassi seguente:  
  
    ```  
    sqlplus system/P@$$W0rd@orcl @"c:\Program Files\Microsoft SQL Server\<InstanceName>\MSSQL\Install\oracleadmin.sql"  
    ```  
  
     In questo esempio, l'account Oracle incorporato **system** viene utilizzato per la connessione a un database Oracle con il nome di rete "orcl".  
  
3.  Quando richiesto, specificare il nome e la password utente e lo spazio di tabella predefinito.  
  
```  
--***********************************************************************  
-- Copyright (c) 2003 Microsoft Corporation  
--  
-- File:  
--  oracleadmin.sql  
--  
-- Purpose:  
-- PL/SQL script to create a database user with the required   
-- permissions to administer SQL Server publishing for an Oracle  
-- database.  
--  
-- &&ReplLogin        == Replication user login  
-- &&ReplPassword     == Replication user password  
-- &&DefaultTablespace == Tablespace that will serve as the default  
-- tablespace for the replication user.  
-- The replication user will be authorized to allocate UNLIMITED space  
-- on the default tablespace, which must already exist.  
--  
-- Notes:  
--  
-- This script must be run from an Oracle login having the  
-- authorization to create a new user and grant unlimited tablespace on  
-- any existing tablespace. The login must also be able to grant to the  
-- newly created login the following authorizations:  
--  
-- create public synonym  
-- drop public synonym  
-- create sequence  
--  create procedure  
-- create session  
-- create table  
-- create view  
--  
-- Additionally, the following properties are also required for  
-- transactional publications.  
--  
-- create any trigger  
--  
--  All of the privileges may be granted through a role, with the  
-- exception of create table, create view, and create any trigger.  
-- These must be granted explicitly to the replication user login.  
-- In the script, all grants are granted explicitly to the replication  
-- user.  
--  
-- In addition to these general grants, a table owner must explicitly  
-- grant select authorization to the replication user on a table before  
-- the table can be published.  
--  
***********************************************************************  
  
ACCEPT ReplLogin CHAR PROMPT 'User to create for replication: ';  
ACCEPT ReplPassword CHAR PROMPT 'Replication user passsword: ' HIDE;  
ACCEPT DefaultTableSpace CHAR DEFAULT 'SYSTEM' PROMPT 'Default tablespace: ';  
  
-- Create the replication user account  
CREATE USER &&ReplLogin IDENTIFIED BY &&ReplPassword DEFAULT TABLESPACE &&DefaultTablespace QUOTA UNLIMITED ON &&DefaultTablespace;  
  
-- It is recommended that only the required grants be granted to this  
-- user.  
--  
-- The following 5 privileges are granted explicitly, but could be  
-- granted through a role.  
GRANT CREATE PUBLIC SYNONYM TO &&ReplLogin;  
GRANT DROP PUBLIC SYNONYM TO &&ReplLogin;  
GRANT CREATE SEQUENCE TO &&ReplLogin;  
GRANT CREATE PROCEDURE TO &&ReplLogin;  
GRANT CREATE SESSION TO &&ReplLogin;  
  
-- The following privileges must be granted explicitly to the  
-- replication user.  
GRANT CREATE TABLE TO &&ReplLogin;  
GRANT CREATE VIEW TO &&ReplLogin;  
  
-- The replication user login needs to be able to create a tracking  
-- trigger on any table that is to be published in a transactional  
-- publication. The CREATE ANY privilege is used to obtain the  
-- authorization to create these triggers.  To replicate a table, the  
-- table owner must additionally explicitly grant select authorization  
-- on the table to the replication user.  
--  
-- NOTE: CREATE ANY TRIGGER is not required for snapshot publications.  
GRANT CREATE ANY TRIGGER TO &&ReplLogin;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un server di pubblicazione Oracle](configure-an-oracle-publisher.md)  
  
  
