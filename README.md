instrument { name = 'TARGET CRUZE 2022',
   icon = 'https://midia.gruposinos.com.br/_midias/jpg/2020/10/21/download-19246341.jpeg',
    overlay = true
}

percentage = input (1, "Percentage", input.double, 1, 100, 3) / 100
period = 5


input_group {
    "front.ind.dpo.generalline",
    up_color = input { default = "", type = input.color },
     width = input { default = 1, type = input.line_width },
    visiblepercentage = input { default = false, type = input.plot_visibility }
}

input_group {
    "front.ind.dpo.generalline",
    down_color = input { default = "", type = input.color },
     width = input { default = 1, type = input.line_width },
    visiblepercentage = input { default = false, type = input.plot_visibility }
}

input_group {"CALL", call_color= input{ default= "rgba(0, 250, 154, 0.80)", type= input.color}}

input_group {"PUT", put_color= input{ default= "rgba(220, 20, 60, 0.8)", type= input.color}}


local reference = make_series ()
reference:set(nz(reference[1], high))
local is_direction_up = make_series ()
is_direction_up:set(nz(is_direction_up[1], true))
local htrack = make_series ()
local ltrack = make_series ()
local pivot = make_series ()
reverse_range = reference * percentage / 100
if get_value (is_direction_up) then
    htrack:set (max(high, nz(htrack[1], high)))
    if close < htrack[1] - reverse_range then
        pivot:set (htrack)
        is_direction_up:set (false)
        reference:set(htrack)
    end
else
    ltrack:set (min(low, nz(ltrack[1], low)))
    if close > ltrack[1] + reverse_range then
        pivot:set (ltrack)
        is_direction_up:set(true)
        reference:set (ltrack)
    end
end
color = is_direction_up() and  up_color or down_color
plot(pivot, 'ZZ', color, width, -1, style.solid_line, na_mode.continue)



smaa= sma(close, '1')
upper_high= smaa + (stdev(close,10) *1 )
lower_high= smaa - (stdev(close,10) *1 )
emaa= ema(close, '')

if Exibir_tracamento == 1 then
plot(emaa, "SMA", ema_color)
plot(upper_high, "UPPER_HIGH", sup_color)
plot(lower_high, "LOWER_HIGH", inf_color)
end

plot_shape((high >= upper_high and emaa > upper_high),
"PUT",
shape_style.arrowdown,
shape_size.huge,
put_color,
shape_location.abovebar,
0,
"CRUZE",
put_color)

plot_shape((low <= lower_high and emaa < lower_high),
"CALL",
shape_style.arrowup,
shape_size.huge,
call_color,
shape_location.belowbar,
0,
"CRUZE",
call_color)



instrument { name = 'TARGET CRUZE 2022',icon='https://midia.gruposinos.com.br/_midias/jpg/2020/10/21/download-19246341.jpeg', overlay = true
}


exibir_tracamento = input ( 1, "Desea exibir?", input.string_selection, {"SI","No"})

input_group { "SMAA", smaa_color = input{ default = "orange", type = input.color }}
input_group { "SMAB", smab_color = input{ default = "rgba(0, 0, 255, 0.8)", type = input.color }}




sec = security(current_ticker_id, "1m")


smaa = ema(close, '10')
smab = ema(close, '20')
smaao = ema(open, '10')
smabo = ema(open, '20')


plot(smaa, "EMA", smaa_color)
plot(smab, "EMA", smab_color)


emaa = ema(close, '20')


period = input (12, "front.period", input.integer, 1)

source = input (1, "front.ind.source", input.string_selection,  inputs.titles)
fn     = input (1, "front.newind.average", input.string_selection, averages.titles)


local sourceSeries = inputs [source]
local averageFunction = averages [fn]

mean = averageFunction (sourceSeries, period)
mad = sourceSeries - mean

rect {
    first = 0,
    second = mad,
    color = mad >= mad [1] and up_color or down_color,
    width = 0.4
}

if
( mad  <= 0 and ( mad[1] > mad) and  (smaa < smab) and (smaao > smabo) and close <= emaa ) then 
plot_shape (1,
"Down",
shape_style.arrowdown,
shape_size.auto,
down_color,
shape_location.abovebar, 
0,
" Down ",
1)
end

if
( mad  >= 0 and (mad > mad[1]) and  (smaa > smab) and close >= emaa and smaao < smabo)
 then 
plot_shape (1 ,
"Up",
shape_style.arrowup,
shape_size.auto,
up_color,
shape_location.belowbar, 
0,
"Up",
1)

end

instrument { name = 'TARGET CRUZE 2022',
   icon = 'https://midia.gruposinos.com.br/_midias/jpg/2020/10/21/download-19246341.jpeg',
    overlay = true
}

percentage = input (1, "Percentage", input.double, 1, 100, 3) / 100
period = 5


input_group {
    "front.ind.dpo.generalline",
    up_color = input { default = "", type = input.color },
     width = input { default = 1, type = input.line_width },
    visiblepercentage = input { default = false, type = input.plot_visibility }
}

input_group {
    "front.ind.dpo.generalline",
    down_color = input { default = "", type = input.color },
     width = input { default = 1, type = input.line_width },
    visiblepercentage = input { default = false, type = input.plot_visibility }
}

input_group {"CALL", call_color= input{ default= "rgba(0, 250, 154, 0.80)", type= input.color}}

input_group {"PUT", put_color= input{ default= "rgba(220, 20, 60, 0.8)", type= input.color}}


local reference = make_series ()
reference:set(nz(reference[1], high))
local is_direction_up = make_series ()
is_direction_up:set(nz(is_direction_up[1], true))
local htrack = make_series ()
local ltrack = make_series ()
local pivot = make_series ()
reverse_range = reference * percentage / 100
if get_value (is_direction_up) then
    htrack:set (max(high, nz(htrack[1], high)))
    if close < htrack[1] - reverse_range then
        pivot:set (htrack)
        is_direction_up:set (false)
        reference:set(htrack)
    end
else
    ltrack:set (min(low, nz(ltrack[1], low)))
    if close > ltrack[1] + reverse_range then
        pivot:set (ltrack)
        is_direction_up:set(true)
        reference:set (ltrack)
    end
end
color = is_direction_up() and  up_color or down_color
plot(pivot, 'ZZ', color, width, -1, style.solid_line, na_mode.continue)



smaa= sma(close, '1')
upper_high= smaa + (stdev(close,10) *1 )
lower_high= smaa - (stdev(close,10) *1 )
emaa= ema(close, '')

if Exibir_tracamento == 1 then
plot(emaa, "SMA", ema_color)
plot(upper_high, "UPPER_HIGH", sup_color)
plot(lower_high, "LOWER_HIGH", inf_color)
end

plot_shape((high >= upper_high and emaa > upper_high),
"PUT",
shape_style.arrowdown,
shape_size.huge,
put_color,
shape_location.abovebar,
0,
"CRUZE",
put_color)

plot_shape((low <= lower_high and emaa < lower_high),
"CALL",
shape_style.arrowup,
shape_size.huge,
call_color,
shape_location.belowbar,
0,
"CRUZE",
call_color)



instrument { name = 'TARGET CRUZE 2022',icon='https://midia.gruposinos.com.br/_midias/jpg/2020/10/21/download-19246341.jpeg', overlay = true
}


exibir_tracamento = input ( 1, "Desea exibir?", input.string_selection, {"SI","No"})

input_group { "SMAA", smaa_color = input{ default = "yellow", type = input.color }}
input_group { "SMAB", smab_color = input{ default = "rgba(0, 0, 255, 0.8)", type = input.color }}




sec = security(current_ticker_id, "1m")


smaa = ema(close, '10')
smab = ema(close, '20')
smaao = ema(open, '10')
smabo = ema(open, '20')


plot(smaa, "EMA", smaa_color)
plot(smab, "EMA", smab_color)


emaa = ema(close, '20')


period = input (12, "front.period", input.integer, 1)

source = input (1, "front.ind.source", input.string_selection,  inputs.titles)
fn     = input (1, "front.newind.average", input.string_selection, averages.titles)


local sourceSeries = inputs [source]
local averageFunction = averages [fn]

mean = averageFunction (sourceSeries, period)
mad = sourceSeries - mean

rect {
    first = 0,
    second = mad,
    color = mad >= mad [1] and up_color or down_color,
    width = 0.4
}

if
( mad  <= 0 and ( mad[1] > mad) and  (smaa < smab) and (smaao > smabo) and close <= emaa ) then 
plot_shape (1,
"Down",
shape_style.arrowdown,
shape_size.auto,
down_color,
shape_location.abovebar, 
0,
" Down ",
1)
end

if
( mad  >= 0 and (mad > mad[1]) and  (smaa > smab) and close >= emaa and smaao < smabo)
 then 
plot_shape (1 ,
"Up",
shape_style.arrowup,
shape_size.auto,
up_color,
shape_location.belowbar, 
0,
"Up",
1)

end
  

instrument { name = 'TARGET CRUZE 2022',
   icon = 'https://midia.gruposinos.com.br/_midias/jpg/2020/10/21/download-19246341.jpeg',
    overlay = true
}

percentage = input (1, "Percentage", input.double, 1, 100, 3) / 100
period = 5


input_group {
    "front.ind.dpo.generalline",
    up_color = input { default = "", type = input.color },
     width = input { default = 1, type = input.line_width },
    visiblepercentage = input { default = false, type = input.plot_visibility }
}

input_group {
    "front.ind.dpo.generalline",
    down_color = input { default = "", type = input.color },
     width = input { default = 1, type = input.line_width },
    visiblepercentage = input { default = false, type = input.plot_visibility }
}

input_group {"CALL", call_color= input{ default= "rgba(0, 250, 154, 0.80)", type= input.color}}

input_group {"PUT", put_color= input{ default= "rgba(220, 20, 60, 0.8)", type= input.color}}


local reference = make_series ()
reference:set(nz(reference[1], high))
local is_direction_up = make_series ()
is_direction_up:set(nz(is_direction_up[1], true))
local htrack = make_series ()
local ltrack = make_series ()
local pivot = make_series ()
reverse_range = reference * percentage / 100
if get_value (is_direction_up) then
    htrack:set (max(high, nz(htrack[1], high)))
    if close < htrack[1] - reverse_range then
        pivot:set (htrack)
        is_direction_up:set (false)
        reference:set(htrack)
    end
else
    ltrack:set (min(low, nz(ltrack[1], low)))
    if close > ltrack[1] + reverse_range then
        pivot:set (ltrack)
        is_direction_up:set(true)
        reference:set (ltrack)
    end
end
color = is_direction_up() and  up_color or down_color
plot(pivot, 'ZZ', color, width, -1, style.solid_line, na_mode.continue)



smaa= sma(close, '1')
upper_high= smaa + (stdev(close,10) *1 )
lower_high= smaa - (stdev(close,10) *1 )
emaa= ema(close, '')

if Exibir_tracamento == 1 then
plot(emaa, "SMA", ema_color)
plot(upper_high, "UPPER_HIGH", sup_color)
plot(lower_high, "LOWER_HIGH", inf_color)
end

plot_shape((high >= upper_high and emaa > upper_high),
"PUT",
shape_style.arrowdown,
shape_size.huge,
put_color,
shape_location.abovebar,
0,
"CRUZE",
put_color)

plot_shape((low <= lower_high and emaa < lower_high),
"CALL",
shape_style.arrowup,
shape_size.huge,
call_color,
shape_location.belowbar,
0,
"CRUZE",
call_color)



instrument { name = 'TARGET CRUZE 2022',icon='https://midia.gruposinos.com.br/_midias/jpg/2020/10/21/download-19246341.jpeg', overlay = true
}


exibir_tracamento = input ( 1, "Desea exibir?", input.string_selection, {"SI","No"})

input_group { "SMAA", smaa_color = input{ default = "orange", type = input.color }}
input_group { "SMAB", smab_color = input{ default = "rgba(0, 0, 255, 0.8)", type = input.color }}




sec = security(current_ticker_id, "1m")


smaa = ema(close, '10')
smab = ema(close, '20')
smaao = ema(open, '10')
smabo = ema(open, '20')


plot(smaa, "EMA", smaa_color)
plot(smab, "EMA", smab_color)


emaa = ema(close, '20')


period = input (12, "front.period", input.integer, 1)

source = input (1, "front.ind.source", input.string_selection,  inputs.titles)
fn     = input (1, "front.newind.average", input.string_selection, averages.titles)


local sourceSeries = inputs [source]
local averageFunction = averages [fn]

mean = averageFunction (sourceSeries, period)
mad = sourceSeries - mean

rect {
    first = 0,
    second = mad,
    color = mad >= mad [1] and up_color or down_color,
    width = 0.4
}

if
( mad  <= 0 and ( mad[1] > mad) and  (smaa < smab) and (smaao > smabo) and close <= emaa ) then 
plot_shape (1,
"Down",
shape_style.arrowdown,
shape_size.auto,
down_color,
shape_location.abovebar, 
0,
" Down ",
1)
end

if
( mad  >= 0 and (mad > mad[1]) and  (smaa > smab) and close >= emaa and smaao < smabo)
 then 
plot_shape (1 ,
"Up",
shape_style.arrowup,
shape_size.auto,
up_color,
shape_location.belowbar, 
0,
"Up",
1)

end



instrument { name = 'TARGET CRUZE 2022',
   icon = 'https://midia.gruposinos.com.br/_midias/jpg/2020/10/21/download-19246341.jpeg',
    overlay = true
}

percentage = input (1, "Percentage", input.double, 1, 100, 3) / 100
period = 5


input_group {
    "front.ind.dpo.generalline",
    up_color = input { default = "", type = input.color },
     width = input { default = 1, type = input.line_width },
    visiblepercentage = input { default = false, type = input.plot_visibility }
}

input_group {
    "front.ind.dpo.generalline",
    down_color = input { default = "", type = input.color },
     width = input { default = 1, type = input.line_width },
    visiblepercentage = input { default = false, type = input.plot_visibility }
}

input_group {"CALL", call_color= input{ default= "rgba(0, 250, 154, 0.80)", type= input.color}}

input_group {"PUT", put_color= input{ default= "rgba(220, 20, 60, 0.8)", type= input.color}}


local reference = make_series ()
reference:set(nz(reference[1], high))
local is_direction_up = make_series ()
is_direction_up:set(nz(is_direction_up[1], true))
local htrack = make_series ()
local ltrack = make_series ()
local pivot = make_series ()
reverse_range = reference * percentage / 100
if get_value (is_direction_up) then
    htrack:set (max(high, nz(htrack[1], high)))
    if close < htrack[1] - reverse_range then
        pivot:set (htrack)
        is_direction_up:set (false)
        reference:set(htrack)
    end
else
    ltrack:set (min(low, nz(ltrack[1], low)))
    if close > ltrack[1] + reverse_range then
        pivot:set (ltrack)
        is_direction_up:set(true)
        reference:set (ltrack)
    end
end
color = is_direction_up() and  up_color or down_color
plot(pivot, 'ZZ', color, width, -1, style.solid_line, na_mode.continue)



smaa= sma(close, '1')
upper_high= smaa + (stdev(close,10) *1 )
lower_high= smaa - (stdev(close,10) *1 )
emaa= ema(close, '')

if Exibir_tracamento == 1 then
plot(emaa, "SMA", ema_color)
plot(upper_high, "UPPER_HIGH", sup_color)
plot(lower_high, "LOWER_HIGH", inf_color)
end

plot_shape((high >= upper_high and emaa > upper_high),
"PUT",
shape_style.arrowdown,
shape_size.huge,
put_color,
shape_location.abovebar,
0,
"CRUZE",
put_color)

plot_shape((low <= lower_high and emaa < lower_high),
"CALL",
shape_style.arrowup,
shape_size.huge,
call_color,
shape_location.belowbar,
0,
"CRUZE",
call_color)



instrument { name = 'TARGET CRUZE 2022',icon='https://midia.gruposinos.com.br/_midias/jpg/2020/10/21/download-19246341.jpeg', overlay = true
}


exibir_tracamento = input ( 1, "Desea exibir?", input.string_selection, {"SI","No"})

input_group { "SMAA", smaa_color = input{ default = "orange", type = input.color }}
input_group { "SMAB", smab_color = input{ default = "rgba(0, 0, 255, 0.8)", type = input.color }}




sec = security(current_ticker_id, "1m")


smaa = ema(close, '10')
smab = ema(close, '20')
smaao = ema(open, '10')
smabo = ema(open, '20')


plot(smaa, "EMA", smaa_color)
plot(smab, "EMA", smab_color)


emaa = ema(close, '20')


period = input (12, "front.period", input.integer, 1)

source = input (1, "front.ind.source", input.string_selection,  inputs.titles)
fn     = input (1, "front.newind.average", input.string_selection, averages.titles)


local sourceSeries = inputs [source]
local averageFunction = averages [fn]

mean = averageFunction (sourceSeries, period)
mad = sourceSeries - mean

rect {
    first = 0,
    second = mad,
    color = mad >= mad [1] and up_color or down_color,
    width = 0.4
}

if
( mad  <= 0 and ( mad[1] > mad) and  (smaa < smab) and (smaao > smabo) and close <= emaa ) then 
plot_shape (1,
"Down",
shape_style.arrowdown,
shape_size.auto,
down_color,
shape_location.abovebar, 
0,
" Down ",
1)
end

if
( mad  >= 0 and (mad > mad[1]) and  (smaa > smab) and close >= emaa and smaao < smabo)
 then 
plot_shape (1 ,
"Up",
shape_style.arrowup,
shape_size.auto,
up_color,
shape_location.belowbar, 
0,
"Up",
1)

end

