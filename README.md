# scrollbar-v2
API de Scrollbar interativa em sua versão 2.0.

## Exemplos / Demonstração
![Preview](https://github.com/ThigasDevelopment/scrollbar-v2/blob/main/preview_scroll.gif)

## Códigos úteis necessários :
```lua
local screen = Vector2 (guiGetScreenSize ()) -- Retorno da Resolução do Client.

function isCursorOnElement (x, y, width, height) -- Verificação do cursor do Client.
    if not isCursorShowing () then
        return false
    end
    
    local cursor = {getCursorPosition ()}
    local cursorx, cursory = (cursor[1] * screen.x), (cursor[2] * screen.y)
    
    return cursorx >= x and cursorx <= (x + width) and cursory >= y and cursory <= (y + height)
end
```
