# europlan
europlan


ну вот пример
ufn bn
drop table if exists #NegativeClient
select
    CR.phone
    ,CR.status
into #NegativeClient
from
    WarehousePG.voipclient_leasing_task T
    join WarehousePG.voipclient_leasing_interaction I
        on I.task = T.id
    right join #Call C
        on C.contact = I.contact and C.CallStarted is not null
    join WarehousePG.voipclient_leasing_call_result CR
        on CR.call_id = C.id
        and CR.[status] in (67, 310)
group by
    CR.phone
    ,CR.status
