---
title: Sottoespressione comuni illustrati nel sistema di piattaforma Analitica | Microsoft Docs
description: Miglioramento delle query di esempio consente di visualizzare che è stato introdotto in CU7.3 sistema di piattaforma Analitica
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 12/17/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 2dd02bed55f3d3781428eae3ec4bc2d0655819ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312464"
---
# <a name="common-subexpression-elimination-explained"></a>Eliminazione di sottoespressioni comuni illustrati

APS CU7.3 migliora le prestazioni delle query con l'eliminazione di sottoespressioni comuni in query optimizer di SQL. Il miglioramento migliora le query in due modi. Il vantaggio prima è la possibilità di identificare ed eliminare tali espressioni consentono di ridurre il tempo di compilazione di SQL. Il vantaggio di secondo e più importante è operazioni di spostamento dei dati per queste sottoespressioni ridondanti sono state eliminate in questo modo il tempo di esecuzione per le query diventa più veloce.

```sql
select top 100 asceding.rnk, i1.i_product_name best_performing, i2.i_product_name worst_performing
  from(select *
       from (select item_sk,rank() over (order by rank_col asc) rnk
             from (select ss_item_sk item_sk,avg(ss_net_profit) rank_col
                   from store_sales ss1
                   where ss_store_sk = 8
                   group by ss_item_sk
                   having avg(ss_net_profit) > 0.9*(select avg(ss_net_profit) rank_col
                                                    from store_sales
                                                    where ss_store_sk = 8
                                                      and ss_hdemo_sk is null
                                                    group by ss_store_sk))V1)V11
       where rnk  < 11) asceding,
      (select *
       from (select item_sk,rank() over (order by rank_col desc) rnk
             from (select ss_item_sk item_sk,avg(ss_net_profit) rank_col
                   from store_sales ss1
                   where ss_store_sk = 8
                   group by ss_item_sk
                   having avg(ss_net_profit) > 0.9*(select avg(ss_net_profit) rank_col
                                                    from store_sales
                                                    where ss_store_sk = 8
                                                      and ss_hdemo_sk is null
                                                    group by ss_store_sk))V2)V21
       where rnk  < 11) descending,
  item i1,
  item i2
  where asceding.rnk = descending.rnk
    and i1.i_item_sk=asceding.item_sk
    and i2.i_item_sk=descending.item_sk
  order by asceding.rnk
  ;
```
Si consideri la query precedente dagli strumenti di benchmark TPC-DS.  Nella query precedente, la sottoquery è lo stesso, ma la clausola order by con rank/routine di funzione viene ordinata in due modi diversi. Precede CU7.3, questa sottoquery otterrà valutata ed eseguita due volte, una volta per ordine crescente e una sola volta per l'ordinamento decrescente, sostenere due operazioni di spostamento dei dati. Dopo aver installato CU7.3 APS, la parte di sottoquery verrà valutata una sola volta in questo modo riducendo lo spostamento dei dati e terminare la query più veloce.

È stata introdotta una [opzione della funzionalità](appliance-feature-switch.md) chiamato 'OptimizeCommonSubExpressions' che consentirà testare la funzionalità anche dopo l'aggiornamento a CU7.3 APS. La funzionalità è attivata per impostazione predefinita ma può essere disattivata. 

> [!NOTE] 
> Modifiche ai valori della funzionalità commutatore richiedono un riavvio del servizio.

È possibile provare la query di esempio crea le tabelle seguenti nell'ambiente di test e valutando il piano explain per la query citato in precedenza. 

```sql
CREATE TABLE [dbo].[store_sales] (
    [ss_sold_date_sk] int NULL, 
    [ss_sold_time_sk] int NULL, 
    [ss_item_sk] int NOT NULL, 
    [ss_customer_sk] int NULL, 
    [ss_cdemo_sk] int NULL, 
    [ss_hdemo_sk] int NULL, 
    [ss_addr_sk] int NULL, 
    [ss_store_sk] int NULL, 
    [ss_promo_sk] int NULL, 
    [ss_ticket_number] int NOT NULL, 
    [ss_quantity] int NULL, 
    [ss_wholesale_cost] decimal(7, 2) NULL, 
    [ss_list_price] decimal(7, 2) NULL, 
    [ss_sales_price] decimal(7, 2) NULL, 
    [ss_ext_discount_amt] decimal(7, 2) NULL, 
    [ss_ext_sales_price] decimal(7, 2) NULL, 
    [ss_ext_wholesale_cost] decimal(7, 2) NULL, 
    [ss_ext_list_price] decimal(7, 2) NULL, 
    [ss_ext_tax] decimal(7, 2) NULL, 
    [ss_coupon_amt] decimal(7, 2) NULL, 
    [ss_net_paid] decimal(7, 2) NULL, 
    [ss_net_paid_inc_tax] decimal(7, 2) NULL, 
    [ss_net_profit] decimal(7, 2) NULL
)
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH([ss_item_sk]),  PARTITION ([ss_sold_date_sk] RANGE RIGHT FOR VALUES (2450815, 2451180, 2451545, 2451911, 2452276, 2452641, 2453006)));

CREATE TABLE [dbo].[item] (
    [i_item_sk] int NOT NULL, 
    [i_item_id] char(16) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, 
    [i_rec_start_date] date NULL, 
    [i_rec_end_date] date NULL, 
    [i_item_desc] varchar(200) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_current_price] decimal(7, 2) NULL, 
    [i_wholesale_cost] decimal(7, 2) NULL, 
    [i_brand_id] int NULL, 
    [i_brand] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_class_id] int NULL, 
    [i_class] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_category_id] int NULL, 
    [i_category] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_manufact_id] int NULL, 
    [i_manufact] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_size] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_formulation] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_color] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_units] char(10) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_container] char(10) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_manager_id] int NULL, 
    [i_product_name] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL
)
WITH (CLUSTERED INDEX ( [i_item_sk] ASC ), DISTRIBUTION = REPLICATE);
```
Se esaminiamo il piano explain della query, si noterà che prima CU7.3 (o quando l'opzione della funzionalità è disattivata) se la query include 17 numero totale di operazioni e dopo CU7.3 (o con l'opzione della funzionalità attivata) della stessa query Mostra 9 numero totale di operazioni. Se si conteggiare solo le operazioni di spostamento dei dati, noterete che il piano precedente ha quattro operazioni di spostamento e due operazioni di spostamento nel nuovo piano. Nuovo query optimizer è stato in grado di ridurre due operazioni di spostamento dei dati usando di nuovo la tabella già stato creato con il nuovo piano riducendo in tal modo il runtime di query. 


