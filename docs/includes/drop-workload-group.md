Elimina un gruppo del carico di lavoro esistente di Resource Governor definito dall'utente.

:::image type="icon" source="../database-engine/configure-windows/media/topic-link.gif"::: [Convenzioni della sintassi Transact-SQL](../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintassi

```syntaxsql
DROP WORKLOAD GROUP group_name
[;]
```

## <a name="arguments"></a>Argomenti

*group_name* è il nome di un gruppo di carico di lavoro esistente definito dall'utente.

## <a name="remarks"></a>Osservazioni

L'istruzione DROP WORKLOAD GROUP non è consentita per i gruppi interni o predefiniti di Resource Governor.

Per l'esecuzione di istruzioni DDL, è consigliabile avere familiarità con gli stati di Resource Governor. Per altre informazioni, vedere [Resource Governor](../relational-databases/resource-governor/resource-governor.md).

Se un gruppo del carico di lavoro contiene sessioni attive, non sarà possibile eliminare o spostare il gruppo del carico di lavoro a un pool di risorse diverso quando l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE dovrà applicare la modifica. Per evitare il problema, eseguire una delle azioni seguenti:

- Attendere la disconnessione di tutte le sessioni relative al gruppo interessato, quindi eseguire nuovamente l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.

- Arrestare in modo esplicito le sessioni del gruppo interessato utilizzando il comando KILL, quindi eseguire nuovamente l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.

- Riavviare il server. Una volta completato il processo di riavvio, il gruppo eliminato non verrà creato e in un gruppo spostato verrà utilizzata la nuova assegnazione del pool di risorse.

- Una volta generata l'istruzione DROP WORKLOAD GROUP, se si decide di non arrestare in modo esplicito le sessioni per applicare la modifica, è possibile ricreare il gruppo utilizzando lo stesso nome presente prima della generazione dell'istruzione DROP, quindi spostando il gruppo al pool di risorse originale. Per applicare le modifiche, eseguire l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione CONTROL SERVER.

## <a name="examples"></a>Esempi

L'esempio seguente illustra come eliminare il gruppo del carico di lavoro denominato `adhoc`.

```
DROP WORKLOAD GROUP adhoc;
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>Vedere anche

- [Resource Governor](../relational-databases/resource-governor/resource-governor.md)
- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-workload-group-transact-sql.md)  
- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../t-sql/statements/alter-resource-governor-transact-sql.md)  