# Bitácora · Práctica 11

## Ejercicio C3 · Lo que la prueba no ve

No es suficiente que todas las imágenes se anuncien como «Imagen del aviso»: una persona que usa TalkBack no sabría qué muestra cada una. La descripción debería distinguir el contenido; por ejemplo, «Imagen del aviso Feria de proyectos». La prueba debe buscar esa descripción específica, no solo comprobar que existe alguna descripción.

## Bloque D · Caza de mutantes

| Mutante | Prueba que lo detecta | Resultado |
| --- | --- | --- |
| 1 · `..` → `until` en el límite del título | `AvisoValidatorTest.un_titulo_de_3_y_uno_de_60_caracteres_son_validos` | La prueba local falla porque un título de 60 caracteres deja de ser válido. |
| 2 · `< 60` → `<= 60` en tiempo relativo | `FormatoTest.a_los_59_minutos_todavia_son_minutos_y_a_los_60_ya_es_una_hora` | La prueba local falla porque a los 60 minutos todavía muestra minutos. |
| 3 · quitar la guarda de `publicar()` | `PublicarViewModelTest.tocar_publicar_dos_veces_manda_un_solo_aviso` | La instrumentada falla: se crean dos avisos en vez de uno. |
| 4 · quitar la descripción de la imagen de `TarjetaAviso` | `PublicarScreenTest.la_imagen_elegida_se_anuncia_y_se_puede_quitar` | La instrumentada falla porque ya no encuentra «Imagen del aviso». |
| 5 · `LADO_MAX` 1280 → 12800 | Sobrevive a las pruebas originales; la detecta `CompresorDeImagenTest.una_foto_grande_sale_con_1280_px_en_su_lado_mas_largo` | Con el mutante, la prueba falla: esperaba 1280 px y recibió 3000 px. |

## Cierre

Con `LADO_MAX` restaurado a 1280, el checkpoint D4 pasó 13 pruebas locales y 13 instrumentadas en el emulador. El experimento con los cinco mutantes se guardó en la rama `experimento-mutantes`; el checkpoint final quedó en `main`.
