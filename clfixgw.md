`client --[FIX]--> clfixgw --[sbe: OCR + ccy=""]--> crossfire --[sbe: OCR + ccy]--> lpfix --[FIX: Currency<15>=ccy]--> lpalgogw --[...]--> JPM`

Current client request
```
     1 Account                      TEST 
     8 BeginString                  FIX.4.4 
     9 BodyLength                   00185 
    10 CheckSum                     248 
   264 MarketDepth                  0 
   269 MdEntryType                  [0, 1] 
   262 MdReqId                      a75ed276-0747-4af1-ac1f-a0be2add3155 
   265 MdUpdateType                 0 
    34 MsgSeqNum                    2 
    35 MsgType                      V (Market Data Request)
   267 NoMdEntryTypes               2 
   146 NoRelatedSym                 1 
   207 SecurityExchange             CTDL 
   167 SecurityType                 SPOTFWD 
    49 SenderCompId                 HAI_MD 
    52 SendingTime                  20241015-11:09:56.362 
   263 SubReqType                   1 
    55 Symbol                       EURUSD 
    56 TargetCompId                 SWITCHBOARD_UAT 
```
Snapshot coming back to client
```
     1 Account                      TEST 
     8 BeginString                  FIX.4.4 
     9 BodyLength                   00334 
    10 CheckSum                     075 
   290 MdEntryPositionNo            [1, 2, 3, 1, 2] 
   270 MdEntryPx                    [1.09158, 1.09157, 1.09156, 1.0917, 1.09171] 
   271 MdEntrySize                  [1000000, 3000000, 5000000, 1000000, 3000000] 
   269 MdEntryType                  [0, 0, 0, 1, 1] 
   262 MdReqId                      a75ed276-0747-4af1-ac1f-a0be2add3155 
    34 MsgSeqNum                    2 
    35 MsgType                      W (Market Data Snapshot)
   268 NoMdEntries                  5 
   537 QuoteType                    4 
   207 SecurityExchange             CTDL 
    49 SenderCompId                 SWITCHBOARD_UAT 
    52 SendingTime                  20241015-11:09:59.439 
    64 SettlDate                    20241017 
    55 Symbol                       EURUSD 
    56 TargetCompId                 HAI_MD 
```
