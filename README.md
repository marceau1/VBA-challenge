# VBA-challenge
VBA Challenge homework
Sub Stock_market_data()
          
'creation of a For Loop yo navigate the the other worksheets
    Dim ws As Worksheet
    For Each ws In Worksheets
    ws.Activate
     
'Assign name to diffentes cells
    
    ws.Cells(1, 9).Value = "Ticker"
    ws.Cells(1, 10).Value = "Yearly Change"
    ws.Cells(1, 11).Value = "Percent Change"
    ws.Cells(1, 12).Value = "Total Stock Volume"
    
    ws.Cells(1, 16).Value = "Ticker"
    ws.Cells(1, 17).Value = "Value"
    ws.Cells(2, 15).Value = "Greatest % Increase"
    ws.Cells(3, 15).Value = "Greatest % Decrease"
    ws.Cells(4, 15).Value = "Greatest Total Volume"
    
'Declaring a variable and assigning the counter for rows in our Summary table
    Dim summary_table_row As Long
    summary_table_row = 2
'Declaring needed variables.
    Dim ticker_name As String
    Dim yearly_change As Double
    Dim percent_change As Double
    Dim open_year As Double
    Dim close_year As Double
    Dim total_volume As Double
    Dim summary_table As Long

'assign number to summary table ane total volume
    'total_volume = 0
    summary_table = 2
    
'Declaration of variables for the greatest values and assign a counter for each
    Dim G_percent_increase As Double
    G_percent_increase = 0
    Dim G_percent_ticker_increase As String
        
    Dim G_percent_decrease As Double
    G_percent_decrease = 0
    Dim G_percent_ticker_decrease As String
    
    Dim G_total_volume As Double
    G_total_volume = 0
    Dim G_total_volume_ticker As String
    
'Declaration of variavle Last_Row(LR)
    Dim LR As String
    LR = Cells(Rows.Count, 1).End(xlUp).Row
    
'MsgBox ("LR")
'Utilisation of a  For_loop that will check every single row in this worksheet

    For j = 2 To LR
'using the conditional formating 
    If Cells(j - 1, 1).Value <> Cells(j, 1).Value Then
    open_year = Cells(j, 3).Value
    End If
'assign value to ticker columm base on the condional formating 
    If Cells(j + 1, 1).Value <> Cells(j, 1).Value Then
    ticker_name = Cells(j, 1).Value
    
'find unique tot value
    ticker_name = Cells(j, 1).Value
    
    total_volume = total_volume + Cells(j, 7).Value
'closing price
   close_year = Cells(j, 6).Value
    'End If
    
'Assign Total volume to our ticker column
    
' MsgBox ("total_volume")

'Closing price at the end of the year

    

'assign data to ticket_name, Yearly_chnage and percent_change
    ws.Range("I" & summary_table).Value = ticker_name
    ws.Range("L" & summary_table).Value = total_volume
    ws.Range("J" & summary_table).Value = close_year - open_year
'ws.Range("K" & summary_table).Value = ((close_year - open_year) / open_year)
    ws.Range("K" & summary_table).Value = ((close_year - open_year) / open_year)

'using the condional formating and add color to cells
    If Range("J" & summary_table).Value > 0 Then
    ws.Range("J" & summary_table).Interior.ColorIndex = 4
    Else
    ws.Range("J" & summary_table).Interior.ColorIndex = 3
    End If

'Using If statements to find the values for the Greatest values table
    If Range("K" & summary_table).Value > G_percent_increase Then
    G_percent_increase = Range("K" & summary_table).Value
    G_total_volume_ticker = ticker_name
    
    End If

    If Range("K" & summary_table).Value < G_percent_decrease Then
    G_percent_decrease = Range("K" & summary_table).Value
    G_percent_ticker_decrease = ticker_name
    End If

    If Range("L" & summary_table).Value > G_total_volume Then
    G_total_volume = Range("L" & summary_table).Value
    G_total_volume_ticker = ticker_name
    End If
    
'incrementation of summary_table data
    summary_table = summary_table + 1
    
    total_volume = 0
    
    Else
    
    total_volume = total_volume + Cells(j, 7).Value
    End If
    Next j
   
   'Range("K2:K" & last_row).NumberFormat = "0.00%"
   'Range("Q2:Q3").NumberFormat = "0.00%"
   
'assign values to the Greatest values table
    ws.Range("P" & 2).Value = G_percent_ticker_increase
    ws.Range("Q" & 2).Value = G_percent_increase
    ws.Range("P" & 3).Value = G_percent_ticker_decrease
    ws.Range("Q" & 3).Value = G_percent_decrease
    ws.Range("P" & 4).Value = G_total_volume_ticker
    ws.Range("Q" & 4).Value = G_total_volume

    summary_table = summary_table + 1
    
    Worksheets(1).Activate
    Worksheets(1).Cells(1, 1).Select

    Next ws
   
   End Sub

