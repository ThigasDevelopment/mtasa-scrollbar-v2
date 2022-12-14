# SISTEMA DE SCROLLBAR
API de Scrollbar em DX interativa em sua versão 2.0

## Licença
Livraria aberta para uso / alterações do mesmo.

## Sobre
Uma livraria aberta para utilizar em suas listas feitas em DX, ela funciona tanto no click, quanto no scroll do mouse.

## Demonstração
![Preview](https://github.com/ThigasDevelopment/scrollbar-v2/blob/main/preview_scrollbar.gif)

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

## Como usar ?
- Faça download do arquivo ```scrollbar.lua``` e adicione no meta da seguinte maneira :
    - na tag `src` indique o diretório do arquivo da scrollbar.
    
    - ### Exemplo

    ```xml
    <script src = 'scrollbar.lua' type = 'client' cache = 'false'/>
    ```
- Exemplo de como utilizar
    ```lua
    local visible = 5

    local itens = {
        'Texto';
        'Texto';
        'Texto';
        'Texto';
        'Texto';
        'Texto';
        'Texto';
        'Texto';
        'Texto';
        'Texto';
        'Texto';
        'Texto';
    }
    
    createScroll ('Testando', {x = 500, y = 500, width = 10, height = 150, size = 35}, {background = {41, 41, 41, 255}, using = {227, 146, 50, 255}, scroll = {73, 73, 73, 255}}, false, function () return true end, 1, itens, visible, false)
    
    addEventHandler ('onClientRender', root, function ()
        local data = getScroll ('Testando')
        
        for i = 1, visible do
            local values = itens[i + data]
            
            if values then
                dxDrawText (values..' '..(i + data), 520, 500, 50, 30, tocolor (255, 255, 255, 255), 1, 'default', 'left', 'top')
            end
        end
    end)
    ```

# Funções

## createScroll

```lua
bool createScroll (id, position, coloration, animation, condition, update, values, visible, postGUI)
```

- [string](https://wiki.multitheftauto.com/wiki/String) `id`: Nome / Identificador da scrollbar.
- [table](https://wiki.multitheftauto.com/wiki/Table) `position`: Posição da scrollbar.
- [table](https://wiki.multitheftauto.com/wiki/Table) `coloration`: Coloração da scrollbar.
- [table](https://wiki.multitheftauto.com/wiki/Table) `animation`: Animação da scrollbar.
- [function](https://wiki.multitheftauto.com/wiki/Function) `condition`: Função de verificação do cursor para utilizar os scrolls do mouse.
- [int](https://wiki.multitheftauto.com/wiki/Int) `update`: Número de atualização da scrollbar.
- [table](https://wiki.multitheftauto.com/wiki/Table) `values`: Tabela de itens da scrollbar.
- [int](https://wiki.multitheftauto.com/wiki/Int) `visible`: Número de itens visiveis na sua scrollbar.
- [boolean](https://wiki.multitheftauto.com/wiki/Boolean) `postGUI`: Pós processamento da scrollbar.

### Exemplo

```lua
local visible = 5

local itens = {
    'Texto';
    'Texto';
    'Texto';
    'Texto';
    'Texto';
    'Texto';
    'Texto';
    'Texto';
    'Texto';
    'Texto';
    'Texto';
    'Texto';
}

local name = 'Exemplo Scrollbar'

createScroll (
    name,
    {x = 500, y = 500, width = 10, height = 150, size = 45},
    {background = {41, 41, 41, 255}, using = {227, 146, 50, 255}, scroll = {73, 73, 73, 255}},
    {start = 0, final = 1, tick = getTickCount (), time = 350}, -- Caso não queira deixe false.
    function () return isCursorOnElement (520, 500, 100, 150) end, -- Caso não queira verificar o cursor, retorne true.
    1, -- Caso queira q a scroll desça de 3 em 3, coloque 3.
    itens,
    visible,
    false
)
```

## destroyScroll

```lua
bool destroyScroll ([id])
```

- [string](https://wiki.multitheftauto.com/wiki/String) `id`: Nome / Identificador da scrollbar.

### Exemplo

```lua
local name = 'Exemplo Scrollbar'

destroyScroll (name) -- Caso não especifique nenhum id, a função destruirá todas as scrollbars.
```

## getScroll

```lua
bool getScroll (id)
```

- [string](https://wiki.multitheftauto.com/wiki/String) `id`: Nome / Identificador da scrollbar.

### Exemplo

```lua
local name = 'Exemplo Scrollbar'

getScroll (name) -- Ouput : 0 ou a posição atual da lista.
```

## setScroll

```lua
bool setScroll (id, value)
```

- [string](https://wiki.multitheftauto.com/wiki/String) `id`: Nome / Identificador da scrollbar.
- [int](https://wiki.multitheftauto.com/wiki/Int) `value`: Valor de atualização da scrollbar.

### Exemplo

```lua
local name = 'Exemplo Scrollbar'

setScroll (name, 1) -- Define a posição da lista na scroll.
```

## animScroll

```lua
bool animScroll (id, start, final, tick)
```

- [string](https://wiki.multitheftauto.com/wiki/String) `id`: Nome / Identificador da scrollbar.
- [int](https://wiki.multitheftauto.com/wiki/Int) `start`: Valor de inicio da animação.
- [int](https://wiki.multitheftauto.com/wiki/Int) `final`: Valor final da animação.
- [int](https://wiki.multitheftauto.com/wiki/Int) `tick`: Tick atual da animação (getTickCount).

### Exemplo

```lua
local name = 'Exemplo Scrollbar'

animScroll (name, 1, 0, getTickCount ())
```

## setScrollValues

```lua
bool setScrollValues (id, values)
```

- [string](https://wiki.multitheftauto.com/wiki/String) `id`: Nome / Identificador da scrollbar.
- [table](https://wiki.multitheftauto.com/wiki/Table) `values`: Tabela de itens da scrollbar.

### Exemplo

```lua
local name = 'Exemplo Scrollbar'

local itens = {
    'Teste';
    'Teste';
    'Teste';
    'Teste';
}

setScrollValues (name, itens) -- Define a posição da lista na scroll.
```
