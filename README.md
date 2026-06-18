# europlan
SELECT DISTINCT
    BL.PhoneNumber,
    T.cta_repository_id
FROM [Custom].[BlackList_ToInsert] BL
JOIN WarehousePG.voipclient_leasing_call_result CR
    ON CR.phone = BL.PhoneNumber
JOIN WarehousePG.voipclient_leasing_interaction I
    ON I.id = CR.interaction
JOIN WarehousePG.voipclient_leasing_task T
    ON T.id = I.task
WHERE BL.InsertReason IN ('ISCC_hang_up_client', 'ISCC_hang_up_lpr')
  AND T.cta_repository_id IS NOT NULL;
