## θ-join
Consente di unire tuple che soddisfano una condizione del tipo:
- AθB
dove
- θ è un operatore di confronto
- A è un attributo dello chema del primo operando
- B è un attributo dello schema del secondo operando
- dom(A) = dom(B)
*r1 >< r2 = σAθB (r1 x r2 )*

esercizio aerei:
- Viaggi_2018 = selezione(VIAGGIO.data >= 01/01/2018 and VIAGGIO.data <= 31/12/2018)
- Anno_norev = selezione(AEREO.dataR = 00/00/00)
- Volo_R = selezione città = Roma (V >< A arrivo= a.sigla)
Volo_R >< viaggi_2018 >< Anno_norev
1) volo_R.sigla = viaggio_2018.sigla.volo
2) AEREO = anno_norev.id
 