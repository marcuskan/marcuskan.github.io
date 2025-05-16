---
layout: post
title:  "Parsing Exchange SMTP logs to find out who's sending through your Exchange Server"
---

# Welcome

**Hello world**, this is my first Jekyll blog post.

<code>  SELECT 
    EXTRACT_PREFIX(remote-endpoint, 0, ':') AS RemoteIP,
    EXTRACT_TOKEN(Data, 1, ' ') AS Hostname,
    COUNT(*) AS OccurrenceCount
INTO 'C:\Users\mkan\OneDrive - MetService\Documents\ExchangeDiscovery\Output\HostsSendingToLegacyServer.csv'
FROM '[LOGFILEPATH]'
WHERE 
    remote-endpoint LIKE '%:%' AND
    Event = '<' AND
    (Data LIKE 'ehlo%' OR Data LIKE 'helo%') AND
    Data LIKE '% %'
GROUP BY 
    EXTRACT_PREFIX(remote-endpoint, 0, ':'),
    EXTRACT_TOKEN(Data, 1, ' ')
ORDER BY 
    OccurrenceCount DESC`
</code>
