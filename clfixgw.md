`client --[FIX]--> clfixgw --[sbe: OCR + ccy=""]--> crossfire --[sbe: OCR + ccy]--> lpfix --[FIX: Currency<15>=ccy]--> lpalgogw --[...]--> JPM`

Current client request
```
crossfire-fix13-513ad5c6de6e 2024/10/15 11:01:06.421853 FIX_MESSAGE <4.4:SWITCHBOARD->MANGROUP_MD_1, ip4://195.162.2.7:50170> incoming: 8=FIX.4.4|9=174|35=V|34=88399|49=MANGROUP_MD_1|52=20241015-11:01:06.421|56=SWITCHBOARD|262=Q1728848312189|263=1|264=0|265=0|20000=20241119|146=1|55=USDCNH|167=FWD|207=SOCG|267=2|269=0|269=1|10=067|
INCOMING             []  <------------ ['V']
     8 BeginString                  FIX.4.4 
     9 BodyLength                   174 
    10 CheckSum                     067 
   264 MarketDepth                  0 
   269 MdEntryType                  [0, 1] 
   262 MdReqId                      Q1728848312189 
   265 MdUpdateType                 0 
    34 MsgSeqNum                    88399 
    35 MsgType                      V (Market Data Request)
   267 NoMdEntryTypes               2 
   146 NoRelatedSym                 1 
   207 SecurityExchange             SOCG 
   167 SecurityType                 FWD 
    49 SenderCompId                 MANGROUP_MD_1 
    52 SendingTime                  20241015-11:01:06.421 
   263 SubReqType                   1 
    55 Symbol                       USDCNH 
    56 TargetCompId                 SWITCHBOARD 
 20000 Tenor                        20241119 
```
