//+------------------------------------------------------------------+
//|                                                       Projectj50 |
//|                   Copyright 2023, Your Name                        |
//|                             https://www.yourwebsite.com            |
//+------------------------------------------------------------------+
#property copyright "Copyright 2023, Your Name"
#property link      "https://www.yourwebsite.com"
#property version   "1.00"
#property strict

// define input parameters
extern double lotsize = 0.5;
extern int stoploss = 50;
extern int takeprofit = 100;
extern double sar_step = 0.02;
extern double sar_maximum = 0.2;
extern double adx_threshold = 25;

extern string CURRENT_MARKET = "USDCHF";

// define variables
int buy_order;
int sell_order;
bool engulfing;

double current_level_line;
double engulfing_line;
double stop_loss;

void OnTick()
{

    // LOWER - 15 Minutes
    double lower_ema8 = iMA(NULL, PERIOD_M5, 8, 0, MODE_EMA, PRICE_CLOSE, 1);
    double lower_ema14 = iMA(NULL, PERIOD_M5, 14, 0, MODE_EMA, PRICE_CLOSE, 1);
    double lower_ema21 = iMA(NULL, PERIOD_M5, 21, 0, MODE_EMA, PRICE_CLOSE, 1);
    double lower_ema50 = iMA(NULL, PERIOD_M5, 50, 0, MODE_EMA, PRICE_CLOSE, 1);
    double lower_ema100 = iMA(NULL, PERIOD_M5, 100, 0, MODE_EMA, PRICE_CLOSE, 1);
    double lower_ema200 = iMA(NULL, PERIOD_M5, 200, 0, MODE_EMA, PRICE_CLOSE, 1);
    double lower_adx = iADX(NULL, PERIOD_M5, 14, PRICE_CLOSE, MODE_MAIN, 1);
    double lower_di_minus = iADX(NULL, PERIOD_M5, 14, PRICE_CLOSE, MODE_MINUSDI, 1);
    double lower_di_plus = iADX(NULL, PERIOD_M5, 14, PRICE_CLOSE, MODE_PLUSDI, 1);
    double lower_sar = iSAR(NULL, PERIOD_M5, sar_step, sar_maximum, 1);
    
    double   lower_heikinOpen  =  iCustom(Symbol(), PERIOD_M5, "\\Market\\Heikin Ashi Premium", false, 4, 1);
    double   lower_heikinHigh  =  iCustom(Symbol(), PERIOD_M5, "\\Market\\Heikin Ashi Premium", false, 5, 1);
    double   lower_heikinLow   =  iCustom(Symbol(), PERIOD_M5, "\\Market\\Heikin Ashi Premium", false, 6, 1);
    double   lower_heikinClose =  iCustom(Symbol(), PERIOD_M5, "\\Market\\Heikin Ashi Premium", false, 7, 1);
    
    double   lower_heikinHighSL = iCustom(Symbol(), PERIOD_M5, "\\Market\\Heikin Ashi Premium", false, 5, 3);
    double   lower_heikinLowSL   =  iCustom(Symbol(), PERIOD_M5, "\\Market\\Heikin Ashi Premium", false, 6, 3);
    
    double   lower_heikinCloseCURRENT =  iCustom(Symbol(), PERIOD_M5, "\\Market\\Heikin Ashi Premium", false, 7, 0);
     
     
    // GETTING LAST FRACTAL UP
    double lower_fractal_up = 0; 
    
    int lower_bars = iBars(NULL, 0);
    
    int lower_idx = 0;
    
    while (lower_fractal_up == 0) {
         
         double lower_fractal_up_temp = iFractals(NULL, PERIOD_M5, MODE_UPPER, lower_idx);
         lower_idx++;
         if (lower_fractal_up_temp != 0) {
               lower_fractal_up = lower_fractal_up_temp;
               lower_idx = 0;
         }
    }
    
    // GETTING LAST FRACTAL DOWN
    double lower_fractal_down = 0;
    
    
    
    while (lower_fractal_down == 0) {
    
         double lower_fractal_down_temp = iFractals(NULL, PERIOD_M5, MODE_LOWER, lower_idx);
         lower_idx++;
         if (lower_fractal_down_temp != 0) {
               lower_fractal_down = lower_fractal_down_temp;
         }
    }
    
    
    
    
    // UPPER - 1 Hour
    double upper_ema8 = iMA(NULL, PERIOD_M15, 8, 0, MODE_EMA, PRICE_CLOSE, 1);
    double upper_ema14 = iMA(NULL, PERIOD_M15, 14, 0, MODE_EMA, PRICE_CLOSE, 1);
    double upper_ema21 = iMA(NULL, PERIOD_M15, 21, 0, MODE_EMA, PRICE_CLOSE, 1);
    double upper_ema50 = iMA(NULL, PERIOD_M15, 50, 0, MODE_EMA, PRICE_CLOSE, 1);
    double upper_ema100 = iMA(NULL, PERIOD_M15, 100, 0, MODE_EMA, PRICE_CLOSE, 1);
    double upper_ema200 = iMA(NULL, PERIOD_M15, 200, 0, MODE_EMA, PRICE_CLOSE, 1);
    double upper_adx = iADX(NULL, PERIOD_M15, 14, PRICE_CLOSE, MODE_MAIN, 1);
    double upper_di_minus = iADX(NULL, PERIOD_M15, 14, PRICE_CLOSE, MODE_MINUSDI, 1);
    double upper_di_plus = iADX(NULL, PERIOD_M15, 14, PRICE_CLOSE, MODE_PLUSDI, 1);
    double upper_sar = iSAR(NULL, PERIOD_M15, sar_step, sar_maximum, 1);
    
    double   upper_heikinOpen  =  iCustom(Symbol(), PERIOD_M15, "\\Market\\Heikin Ashi Premium", false, 4, 1);
    double   upper_heikinHigh  =  iCustom(Symbol(), PERIOD_M15, "\\Market\\Heikin Ashi Premium", false, 5, 1);
    double   upper_heikinLow   =  iCustom(Symbol(), PERIOD_M15, "\\Market\\Heikin Ashi Premium", false, 6, 1);
    double   upper_heikinClose =  iCustom(Symbol(), PERIOD_M15, "\\Market\\Heikin Ashi Premium", false, 7, 1);
    
    double   upper_heikinHighSL = iCustom(Symbol(), PERIOD_M15, "\\Market\\Heikin Ashi Premium", false, 5, 2);
    double   upper_heikinLowSL   =  iCustom(Symbol(), PERIOD_M15, "\\Market\\Heikin Ashi Premium", false, 6, 2);
    
    
    
    
    
    // GETTING LAST FRACTAL UP
    double upper_fractal_up = 0; 
    
    int upper_bars = iBars(NULL, 0);
    
    int upper_idx = 0;
    
    while (upper_fractal_up == 0) {
         
         double upper_fractal_up_temp = iFractals(NULL, PERIOD_M15, MODE_UPPER, upper_idx);
         upper_idx++;
         if (upper_fractal_up_temp != 0) {
               upper_fractal_up = upper_fractal_up_temp;
               upper_idx = 0;
         }
    }
    
    // GETTING LAST FRACTAL DOWN
    double upper_fractal_down = 0;
    
    
    
    while (upper_fractal_down == 0) {
    
         double upper_fractal_down_temp = iFractals(NULL, PERIOD_M15, MODE_LOWER, upper_idx);
         upper_idx++;
         if (upper_fractal_down_temp != 0) {
               upper_fractal_down = upper_fractal_down_temp;
         }
    }
    
   

    //---
    //Alert("Fractal Up Value: " + fractal_up + "\n" + "Fractal Down Value: " + fractal_down + "\n" + "ema 200 " + ema200 + "\n" + "ema 100 " + ema100 + "\n" + "ema 50 " + ema50 + "\n" + "ema 21 " + ema21 + "\n" + "ema 14 " + ema14 + "\n" + "ema 8 " + ema8 + "\n" + "adx " + adx + "\n" + "di munis " + di_minus + "\n" + "di plus " + di_plus + "\n" + "sar " + sar + "\n" + "Heiken open " + heikinOpen + "\n" + "Heiken close " + heikinClose + "\n" + "Heiken low " + heikinLow + "\n" + "Heiken high " + heikinHigh + "\n" + "Heiken High 2 behind " + heikinHighSL + "\n" + "Heiken Low 2 behind " + heikinLowSL);

    
    if (OrderSelect(0, SELECT_BY_POS)) {
      if (OrderType() == 0) {
         if (lower_heikinClose < current_level_line) {
            
            bool orderClosed = OrderClose(OrderTicket(), lotsize, Ask, 0, Yellow);
            //if (orderClosed) {
               Alert("Order " + OrderTicket() + " Closed: - Price Closed Under The Level Line");
            //}
            buy_order = 0;
            current_level_line = NULL;
            engulfing_line = NULL;
            stop_loss = NULL;
         } else if (lower_heikinCloseCURRENT < stop_loss) {
            bool orderClosed = OrderClose(OrderTicket(), lotsize, Ask, 0, Yellow);
            //if (orderClosed) {
               Alert("Order " + OrderTicket() + " Closed: - Price Hit The Stop Loss");
            //}
            buy_order = 0;
            current_level_line = NULL;
            engulfing_line = NULL;
            stop_loss = NULL;
         } else if (lower_heikinClose > engulfing_line) {
            stop_loss = current_level_line;
            current_level_line = lower_heikinLow;
            engulfing_line = lower_heikinHigh;
            if (current_level_line && Symbol() == "EURJPY") {
               Alert(Symbol() + "\nLevel Line: " + current_level_line + "\nContinuation Line: " + engulfing_line);
            }
         }
         
      } else if (OrderType() == 1) {
         if (lower_heikinClose > current_level_line) {
            bool orderClosed = OrderClose(OrderTicket(), lotsize, Ask, 0, Green);
            //if (orderClosed) {
               Alert("Order " + OrderTicket() + " Closed: - Price Closed Above The Level Line");
            //}
            sell_order = 0;
            current_level_line = NULL;
            engulfing_line = NULL;
            stop_loss = NULL;
         } else if (lower_heikinCloseCURRENT > stop_loss) {
            bool orderClosed = OrderClose(OrderTicket(), lotsize, Ask, 0, Yellow);
            //if (orderClosed) {
               Alert("Order " + OrderTicket() + " Closed: - Price Hit The Stop Loss");
            //}
            buy_order = 0;
            current_level_line = NULL;
            engulfing_line = NULL;
            stop_loss = NULL;
         } 
         else if (lower_heikinClose < engulfing_line) {
            stop_loss = current_level_line;
            current_level_line = lower_heikinHigh;
            engulfing_line = lower_heikinLow;
            if (current_level_line && Symbol() == "EURJPY") {
               Alert(Symbol() + "\nLevel Line: " + current_level_line + "\nContinuation Line: " + engulfing_line);
            }
         }
      }
    } 
    
    // check for buy conditions
    if (upper_ema8 > upper_ema14 && upper_ema14 > upper_ema21 && upper_ema21 > upper_ema50 && upper_ema50 > upper_ema100 && upper_ema100 > upper_ema200 && upper_adx > adx_threshold && upper_di_minus < adx_threshold && upper_heikinOpen > upper_sar && upper_heikinClose > upper_heikinOpen && upper_heikinClose > upper_fractal_up)
    {
        // check if there is no existing buy order
            // check lower timeframe
            if (lower_ema8 > lower_ema14 && lower_ema14 > lower_ema21 && lower_ema21 > lower_ema50 && lower_ema50 > lower_ema100 && lower_ema100 > lower_ema200 && lower_adx > adx_threshold && lower_di_minus < adx_threshold && lower_heikinOpen > lower_sar && lower_heikinClose > lower_heikinOpen && lower_heikinClose > lower_fractal_up)
            {
               if (buy_order == 0)
               {
                  stop_loss = lower_heikinLow;
                  current_level_line = lower_heikinLow;
                  engulfing_line = lower_heikinHigh;
                  buy_order = OrderSend(Symbol(), OP_BUY, lotsize, Ask, 0, lower_heikinLowSL, 0, "Buy", 0, 0, Blue);
               }
            }
    }
    if (upper_ema8 < upper_ema14 && upper_ema14 < upper_ema21 && upper_ema21 < upper_ema200 && upper_adx > adx_threshold && upper_di_plus < adx_threshold && upper_heikinClose < upper_sar && upper_heikinClose < upper_heikinOpen && upper_heikinClose < upper_fractal_down) {
         
         // check if there is no existing sell order
         if (sell_order == 0)
        {
            // check lower timeframe
            if (lower_ema8 < lower_ema14 && lower_ema14 < lower_ema21 && lower_ema21 < lower_ema200 && lower_adx > adx_threshold && lower_di_plus < adx_threshold && lower_heikinClose < lower_sar && lower_heikinClose < lower_heikinOpen && lower_heikinClose < lower_fractal_down)
            {
               stop_loss = lower_heikinHigh;
               current_level_line = lower_heikinHigh;
               engulfing_line = lower_heikinLow;
               sell_order = OrderSend(Symbol(), OP_SELL, lotsize, Ask, 0, upper_heikinLowSL, 0, "Sell", 0, 0, Red);
            }
        }
    }
    //if (current_level_line && Symbol() == "EURJPY") {
    //  Alert(Symbol() + "\nLevel Line: " + current_level_line + "\nContinuation Line: " + engulfing_line);
    //}
    //buy_order = OrderSend(Symbol(), OP_BUY, lotsize, Ask, 0, upper_heikinLowSL, 0, "Buy", 0, 0, Blue);
}

//buy_order = OrderSend(Symbol(), OP_BUY, lotsize, Ask, 0, upper_heikinLowSL, 0, "Buy", 0, 0, Blue);
