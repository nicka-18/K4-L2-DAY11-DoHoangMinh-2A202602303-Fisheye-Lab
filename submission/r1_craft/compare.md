# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_128310.jpg
- L5+R4 center WRONG_CLASS
## adasind_140160.jpg
- L1+R1 edge ATTRIBUTE
## adasind_230910.jpg
- L3+R11 center BOX_GEOMETRY
- L6+R7 mid WRONG_CLASS
- R8 mid MISSING
- R10 center MISSING

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 8 | 5 | 3 | 2 |
| mid | 9 | 7 | 2 | 1 |
| edge | 3 | 3 | 0 | 0 |
