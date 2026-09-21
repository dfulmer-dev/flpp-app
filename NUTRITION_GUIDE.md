# FLPP Smart Nutrition Guide & AI Coaching Framework
**Phase 2: Intelligent meal recommendations based on your personal health profile and daily context**

---

## YOUR PERSONALIZED HEALTH PROFILE

**Key Health Goals:**
- Cardiovascular health protection (familial hypercholesterolemia)
- Lean muscle gain (training with Zone 2 cycling)
- Weight management (caloric balance around training)
- Smoking reduction support (nutrition for stress management)

**Nutritional Targets (Daily):**
- **Protein:** 160-180g (priority for muscle building)
- **Calories:** 2,200-2,500 (adjust based on bike/rest day)
- **Saturated Fat:** <25g (cardiovascular protection)
- **Fiber:** 30-40g (cholesterol management + fullness)
- **Sodium:** <2,500mg (hypertension prevention)

**Contraindications:**
- ❌ High saturated fat meals (avoid Alfredo, fried preparations)
- ❌ Excessive sodium (limit fast-food daily)
- ❌ Ultra-processed foods (prioritize whole foods)
- ✅ Lean proteins (chicken, fish, pork, beef)
- ✅ Grilled/baked preparations
- ✅ Whole grains and vegetables

---

## SMART RECOMMENDATION ENGINE

### Algorithm: Multi-Factor Decision System

**Input Variables:**
1. **Day Type** (Detected from previous logs)
   - Bike Day (Zone 2 cycling completed)
   - Rest Day (No cycling)
   - High-Intensity Day (Future: HIIT or climbing)

2. **Meal Timing** (When user is logging)
   - Breakfast (5am - 11am)
   - Lunch (11am - 2pm)
   - Dinner (5pm - 9pm)
   - Snack (Other times)

3. **Daily Progress** (Accumulated from previous logs)
   - Total protein so far today
   - Total calories consumed
   - Calorie deficit/surplus
   - Water intake

4. **Personalized Context**
   - Recent performance metrics (last 7 days)
   - Mood/Energy level (from health metrics)
   - Sleep quality (previous night)
   - Stress level (smoking data)

### Recommendation Logic

#### **ON BIKE DAYS (High Energy Expenditure)**
**Goal: 2,400-2,700 calories, 180-200g protein, carbs 250-300g**

**Breakfast Recommendation:**
```
IF user_protein_today < 50g AND user_calories < 600:
  RECOMMEND: Panera Turkey Sandwich (900 cal, 43g protein)
  OR: Bonos 4oz Pork Sandwich + toast (500 cal, 35g protein)
  REASON: "Fuel for your bike ride - you'll burn significant calories"
  
ELSE IF quick_breakfast_needed AND time < 7am:
  RECOMMEND: Chick-fil-A Combo (460 cal, 28g protein)
  OR: Bagels R Us Egg & Cheese (475 cal, 23g protein)
  REASON: "Quick portable fuel; easy on the stomach before ride"
```

**Lunch Recommendation (Post-Bike):**
```
IF bike_duration > 90_minutes:
  RECOMMEND: LongHorn Filet 9oz + Sides (650 cal, 52g protein)
  OR: Miller's Osso Buco (1,380 cal, 100g protein) - Major refuel
  REASON: "Your long ride depleted glycogen; prioritize recovery"
  
ELSE IF bike_duration < 60_minutes:
  RECOMMEND: Rice Bowl Pho (500 cal, 30g protein)
  OR: Darumas Hibachi (750 cal, 45g protein)
  REASON: "Moderate ride - lighter refuel with quality protein"
```

**Dinner Recommendation:**
```
IF user_protein_today < 140g:
  RECOMMEND: Miller's Osso Buco (1,380 cal, 100g protein) if not eaten yet
  OR: LongHorn Filet (650 cal, 52g protein)
  REASON: "You need 40-60g more protein to hit daily target"
  
ELSE IF user_protein_today >= 160g AND calories_under_budget:
  RECOMMEND: Salsas Carne Asada Tacos (300-500 cal, 30g protein)
  OR: Pho (400-550 cal, 30g protein)
  REASON: "You've earned lighter dinner; maintain quality protein"
```

---

#### **ON REST DAYS (Lower Energy Expenditure)**
**Goal: 2,000-2,300 calories, 160-180g protein, focus on lean options**

**Strategic Goal: Maintain muscle while creating modest calorie deficit**

**Breakfast Recommendation:**
```
IF user_mood == "low" OR user_energy < 4:
  RECOMMEND: Bagels R Us Egg & Cheese (475 cal, 23g protein)
  OR: Tropical Smoothie Quesadilla (540 cal, 31g protein)
  REASON: "You need energy boost; this will help mood and focus"
  
ELSE:
  RECOMMEND: Olive Garden Grilled Chicken + Toast (350 cal, 25g protein)
  OR: Bonos Pork Sandwich (340 cal, 30g protein)
  REASON: "Lean start to rest day; sets up for leaner remaining meals"
```

**Lunch Recommendation:**
```
IF saturated_fat_today > 20g:
  RECOMMEND: Rice Bowl Pho (400-550 cal, 30g protein)
  OR: Darumas Hibachi Chicken (700 cal, 45g protein)
  REASON: "Watch fat intake on rest day - go lean today"
  
ELSE IF calories_available > 600:
  RECOMMEND: Panera Salad with Protein (500 cal, 40g protein)
  OR: Salsas Carne Asada (400 cal, 25g protein, 2-3 tacos)
  REASON: "Balanced option with vegetables and quality protein"
  
ELSE:
  RECOMMEND: Arby's Roast Beef (360 cal, 23g protein)
  REASON: "Lighter option keeps you on budget"
```

**Dinner Recommendation:**
```
IF user_protein_today < 130g:
  RECOMMEND: LongHorn Filet 6oz + Sides (650 cal, 52g protein)
  OR: Bonos Salad with Pork (530 cal, 53g protein) if lighter preferred
  REASON: "You need 30-50g more protein; lean steaks are perfect"
  
ELSE IF calories_remaining < 500:
  RECOMMEND: Rice Bowl Pho (400 cal, 30g protein)
  OR: Arby's Roast Beef (360 cal, 23g protein)
  REASON: "You're nearing your calorie budget; go light but protein-dense"
  
ELSE:
  RECOMMEND: Darumas Hibachi (750 cal, 45g protein)
  REASON: "You have room; get excellent protein and enjoy variety"
```

---

### Context-Based Fine-Tuning

#### **Smoking Reduction Support**
```
IF cigarettes_logged_today > user_average:
  RECOMMEND: High-protein meal (>40g protein)
  REASON: "Stress eating is normal; prioritize protein for satiety"
  TIMING: Offer as snack or meal within 2 hours of smoking urge
  
  INCLUDE: Protein shake (200 cal, 25g protein)
  OR: Greek yogurt (140 cal, 20g protein)
  SUGGESTION: "Protein helps stabilize blood sugar; snack now"
```

#### **Low Energy Detection**
```
IF user_energy_rating < 3 AND sleep_last_night < 6_hours:
  RECOMMEND: Carb + Protein combo
  MEALS: Panera Turkey Sandwich, Bonos Pork Hawg, or Tijuana Flats Burrito
  REASON: "You need carbs + protein for sustained energy this low-sleep day"
  
ELSE IF user_energy_rating < 3:
  RECOMMEND: High-protein, easy digestion
  MEALS: Greek Yogurt, Protein Shake, or Chick-fil-A Combo
  REASON: "Protein boosts neurotransmitters; may improve mood"
```

#### **Cardiovascular Health Check**
```
IF saturated_fat_weekly > 150g:
  FLAG: "Watch fat intake - you're over target this week"
  RECOMMEND: Lean options for remaining meals
  MEALS: Pho, Grilled Chicken, Fish options
  
IF sodium_weekly > 15000mg:
  FLAG: "Your sodium is high - could affect blood pressure"
  RECOMMEND: Lower-sodium restaurants next week
  ALTERNATIVES: Home-cooked or lighter restaurant meals
```

---

## CUSTOM MEAL CALCULATION METHODOLOGY

### Step 1: Identify Meal Components
Every meal can be broken into:
1. **Protein Source** (primary)
2. **Carb Source** (primary)
3. **Fat Source** (inherent + added)
4. **Vegetables/Fiber** (supporting)

### Step 2: Lookup or Estimate Macronutrients

**For Restaurant Items IN DATABASE:**
- Use exact values from RESTAURANTS.md
- Flag any high sodium or saturated fat

**For Restaurant Items NOT in Database:**
- Use category averages from database
- Example: "Chicken pasta unknown brand" → estimate as Panera average (45g protein, 80g carbs, 30g fat)
- FLAG: Estimated nutrition - suggest looking up exact value

**For Home-Cooked Meals:**
- Use USDA FoodData Central as reference
- Calculate from ingredient sum
- Example: 3oz grilled chicken (105 cal, 26g protein) + 1 cup rice (200 cal, 45g carbs) + 1 tsp oil (40 cal, 4.5g fat) = 345 cal, 26g protein, 49g carbs, 4.5g fat

### Step 3: Calculate Daily Impact

```python
daily_totals = {
  calories: sum(meal_calories),
  protein: sum(meal_protein),
  carbs: sum(meal_carbs),
  fat: sum(meal_fat),
  sat_fat: sum(meal_saturated_fat),
  sodium: sum(meal_sodium),
  fiber: sum(meal_fiber)
}

remaining_budget = {
  calories: 2500 - daily_totals.calories,
  protein: 180 - daily_totals.protein,
  carbs: 300 - daily_totals.carbs,  # Bike day; 250 rest day
  fat: 70 - daily_totals.fat,
  sat_fat: 25 - daily_totals.sat_fat,
  sodium: 2500 - daily_totals.sodium
}
```

### Step 4: Generate AI-Powered Recommendation

**Decision Tree:**
```
IF next_meal == "breakfast":
  IF remaining_protein > 30 AND calories_available > 400:
    → RECOMMEND: High-protein breakfast options
  ELSE:
    → RECOMMEND: Lighter breakfast option

IF next_meal == "lunch":
  IF bike_today:
    → RECOMMEND: High carb + protein for refuel
  ELSE:
    → RECOMMEND: Balanced or high-protein, lower carb

IF next_meal == "dinner":
  IF daily_protein_gap > 30:
    → RECOMMEND: Highest protein option that fits calorie budget
  ELSE:
    → RECOMMEND: Quality protein, moderate option

IF next_meal == "snack":
  IF late_evening AND daily_calories_near_budget:
    → RECOMMEND: Protein only, minimal carbs (protein shake)
  ELSE:
    → RECOMMEND: Protein + carb snack if energy deficit
```

---

## MACRO-CYCLING FOR SPECIAL SCENARIOS

### Post-Bike Recovery Meal (Completed Zone 2 >90 min)
**Timing:** Within 30-60 minutes of ride completion
**Goal:** 25-30g carbs + 20-25g protein

**Formula:**
- Carb: Rice, pasta, bread, potato (45-60g if heavy ride)
- Protein: Chicken, beef, fish (25-35g)
- Fat: Keep low in post-workout window (under 20g)

**Recommendations:**
1. **Miller's Osso Buco (1,380 cal, 100g protein, 120g carbs)** → BEST if main post-bike meal
2. **Bonos Pork Hawg + Apple (600 cal, 50g protein, 85g carbs)** → Good refuel
3. **Rice Bowl Beef Pho (500 cal, 30g protein, 40g carbs)** → Lighter recovery
4. **Panera Turkey Sandwich (900 cal, 43g protein, 95g carbs)** → Balanced refuel

### Pre-Bike Fuel (Planned Zone 2 bike that evening)
**Timing:** 2-3 hours before ride
**Goal:** 30-40g carbs + 10-15g protein (light)

**Recommendations:**
1. **Bagels R Us Egg & Cheese (475 cal, 23g protein, 48g carbs)** → Good breakfast fuel
2. **Toast + Peanut Butter + Banana** → Simple, quick
3. **Protein Shake + Oatmeal** → Smooth digestion

---

## WEEKLY MEAL VARIETY TRACKING

**System monitors (auto-calculated):**
```
Weekly_Restaurant_Count = 5+ unique restaurants
Weekly_Protein_Sources = Beef, Chicken, Pork, Fish, Eggs (all present)
Weekly_Carb_Variety = Rice, Pasta, Bread, Potato, Vegetables
Weekly_Fat_Distribution = Saturated <30%, Unsaturated >60%
```

**AI Alert:** "You've eaten at 3 restaurants this week. Try something new: Rice Bowl or Panera haven't appeared yet."

---

## MEAL LOGGING SHORTCUTS (Phase 2 Feature)

### Quick Log Buttons (Pre-filled)
- **Bike Day + High Hunger** → Suggests: Osso Buco, Pork Hawg, or Double Filet
- **Rest Day + Limited Time** → Suggests: Arby's, Chick-fil-A, or Bagels R Us
- **Post-Workout** → Suggests: Pho, Rice & Protein, or Recovery Sandwich
- **Light Day** → Suggests: Salad, Grilled Chicken, or Pho

### Custom Entry Fields
- Restaurant name (with autocomplete from RESTAURANTS.md)
- Dish name (with calorie lookup if available)
- Portion size (if different from standard)
- Modifications (no oil, extra protein, etc.)
- Custom macro override (if user knows exact values)

---

## SMOKE-QUITTING NUTRITIONAL SUPPORT

**Evidence-Based Strategy:**
- **Protein stabilizes blood sugar** (reduces cravings)
- **Healthy carbs support serotonin** (mood boost)
- **Hydration curbs urges** (replace hand-to-mouth habit)

### Recommendations When Smoking Urge Detected
```
IF time_since_last_cigarette < 60_minutes:
  URGENT: "Nicotine withdrawal spike expected in 15-30 min"
  
  IMMEDIATE SNACK: Protein shake (200 cal, 25g protein)
  REASON: "Quick protein stabilizes dopamine; sips = hand-to-mouth"
  
  NEXT 2 HOURS: Walk + hydration
  MEAL: Full balanced meal at next scheduled time
  
  LOGGING: Flag as "smoke reduction support meal"
```

---

## DATA PRIVACY & SECURITY

**What's Stored Locally (on your device):**
- Daily meal logs
- Exercise data (bike stats)
- Smoking logs
- Health metrics (mood, energy, sleep)

**What Syncs to Google Sheets:**
- Same data as above (for backup/analysis)
- NO cloud processing of sensitive health info
- All data remains under your control

**What Claude AI Never Sees (per privacy rules):**
- Your specific health diagnoses
- Your cardiovascular metrics
- Medication names/dosages
- Detailed smoking history (only aggregate counts)

**What Claude AI Uses (from your health profile):**
- General health goals (muscle, cardiovascular)
- Dietary preferences
- Restaurant preferences
- Calorie/macro targets

---

## ACCURACY & IMPROVEMENT

### Calibration Over Time
- **Week 1:** System uses average nutrition data
- **Week 2:** Learns your restaurant preferences, portion sizes
- **Week 3:** Predicts meals with 80%+ accuracy
- **Month 2+:** Makes personalized recommendations (e.g., "Knows you prefer chicken over beef")

### User Feedback Loop
- Rate recommendation quality: ⭐ - ⭐⭐⭐⭐⭐
- Correction: "Actually had smaller portion" (auto-adjusts future estimates)
- Custom note: "Felt great on this meal; suggest again"
- → System learns and improves

---

## FUTURE FEATURES (Phase 3+)

- ✅ **Barcode Scanning** - Instant nutrition lookup
- ✅ **Photo Recognition** - AI identifies meals in photos
- ✅ **Voice Logging** - "Log: Grilled chicken sandwich and apple"
- ✅ **Wearable Integration** - Auto-import calories from Apple Watch/Fitbit
- ✅ **Smart Reminders** - "You haven't logged lunch; based on typical week, suggest..."
- ✅ **Grocery Integration** - Shop for meal prep ingredients
- ✅ **Cooking Recipes** - Macro-tracked recipes for home cooking
- ✅ **Coach ChatBot** - "Ask Claude" for nutrition questions

---

## QUICK START: USING PHASE 2

### For Each Meal:
1. **Select Restaurant** (or "Home Cooked")
2. **Select Meal** (auto-populated from RESTAURANTS.md)
3. **Confirm Portions** (adjust if different from standard)
4. **Save** (logs nutrition, shows daily progress, displays recommendation for next meal)

### View Recommendations:
- **Before eating:** See suggestions for upcoming meals
- **During day:** Track protein/calorie progress toward daily goal
- **After eating:** View how meal impacted daily totals
- **Weekly:** See variety, nutritional balance, progress toward fitness goals

---

*Last Updated: 2026-09-20*
*Framework designed specifically for Dan's health goals: cardiovascular protection + lean muscle building + smoking reduction*
*All recommendations prioritize long-term health over quick fixes*
