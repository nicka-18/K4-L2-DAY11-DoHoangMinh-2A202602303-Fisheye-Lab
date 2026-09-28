# L / R / M

L/R/M là thứ tự box in-scope theo XML của từng frame.

## adasind_128310.jpg
- L2+R1+M2: LRM (center)
- L3+R2+M1: LRM (edge)
- L4+R5: LR_noM (mid)
- L1+R3+M3: LRM (mid)
- L5: L_only (center)
- R4+M6: RM_noL (center)
- M4: M_only (center)
## adasind_140160.jpg
- L2+R3: LR_noM (center)
- L1+R1: LR_noM (edge)
- L3+R2+M4: LRM (mid)
- M1: M_only (edge)
- M2: M_only (edge)
- M3: M_only (center)
- M5: M_only (center)
- M6: M_only (mid)
## adasind_230910.jpg
- L4+R6+M6: LRM (edge)
- L1+R9+M5: LRM (center)
- L8+R1+M1: LRM (mid)
- L2+R4+M7: LRM (center)
- L5+R5: LR_noM (mid)
- L9+R2+M4: LRM (mid)
- L7+R3+M3: LRM (center)
- L10+R12+M10: LRM (mid)
- L3: L_only (center)
- L6+M9: LM_noR (mid)
- R7: R_only (mid)
- R8: R_only (mid)
- R10: R_only (center)
- R11: R_only (center)
- M8: M_only (mid)

## Zone × cell
| zone | LRM | LR_noM | LM_noR | L_only | RM_noL | R_only | M_only |
|---|---|---|---|---|---|---|---|
| center | 4 | 1 | 0 | 2 | 1 | 2 | 3 |
| mid | 5 | 2 | 1 | 0 | 0 | 2 | 2 |
| edge | 2 | 1 | 0 | 0 | 0 | 0 | 2 |
