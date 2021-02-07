<div dir="auto">

# פרוטוקול הUu


</div>

```mermaid

graph LR
subgraph Uu Protocol
  UE--e-Uu interface---eNodeB
end
  eNodeB--S1-AP---MME
  MME--S6a---HSS
  eNodeB--GTP-U---S-GW
  S-GW--S11---MME
  S-GW--S5/S8---P-GW
  P-GW--IP---IP_NETWORK["IP Networks"]


```

<div dir="auto">

## הקדמה
פרוטוקול הUu הוא הפרוטוקול המקשר בין מכשיר קצה, הטלפון הסלולארי, לבין התא שמשרת אותו.
פרוטוקול זה עובר מעל תווך אווירי.

## שכבות

</div>

```mermaid
graph TB
subgraph L3
  NAS["Non Access Stratum (NAS)"]
  RRC["Radio Resource Control (RRC)"]
  IP["Internet Protocol (IP)"]
end
subgraph L2
  PDCP["Packet Data Convergence Protocol (PDCP)"]
  RLC["Radio Link Control (RLC)"]
  MAC["Medium Access Layer (MAC)"]
end
subgraph L1
  PHY[Physical Layer]
end
  NAS --- RRC
  RRC --- PDCP
  RRC --- RLC
  RRC --- MAC
  IP --- PDCP
  PDCP --- RLC
  RLC --- MAC
  MAC --- PHY
```

<div dir="rtl">

### השכבה הפיזית

השכבה הפיזית מספקת לשכבה מעליה את אפיקי התעבורה הבאים
- BCH
- DL-SCH 
- PCH
- UL-SCH
- RACH
- MCH
- SL-BCH
- SL-DCH
- SL-SCH

</div>
<br>
<div dir="rtl">


### שכבת הMAC
שכבת הMAC אחראית בעיקר למיפוי בין אפיקי תעבורה לאפיקים לוגים.
שכבת הMAC מספקת לשכבות שמעליה גישה לאפיקים הלוגים הבאים:

</div>

- BCCH (Broadcast Control Channel)
- PCCH (Paging Control Channel)
- CCCH (Common Control Channel)
- DCCH (Dedicated Control Channel)
- MCCH (Multicast Control Channel)
- DTCH (Dedicated Traffic Channel)
- MTCH (Multicast Traffic Channel)
- STCH (Sidelink Traffic Channel)
- SBCCH (Sidelink Broadcast Control Channel)


<div dir="rtl">
כאשר האפיקים הלוגים מורכבים מהאפיקי התעבורה הבאים:
</div>

```mermaid
graph TB
subgraph Logical channels["אפיקים לוגים"]
CCCH
DCCH
DTCH
BCCH
PCCH
MCCH
MTCH
STCH
SBCCH
end
subgraph Transport channels["אפיקי תעבורה"]
RACH
UL-SCH
DL-SCH
BCH
PCH
MCH
SL-DCH
SL-SCH
SL-BCH
end
CCCH --- UL-SCH
DCCH --- UL-SCH
DTCH --- UL-SCH
MCCH --- MCH
MTCH --- MCH
PCCH --- PCH
BCCH --- BCH
BCCH --- DL-SCH
CCCH --- DL-SCH
DCCH --- DL-SCH
DTCH --- DL-SCH
SBCCH --- SL-BCH
STCH --- SL-SCH
```