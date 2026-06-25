# پکیج Codex برای سیستم حرفه‌ای Multi-Agent Workout Planner

این پکیج برای ساخت یک سیستم حرفه‌ای تولید برنامه ورزشی چندایجنتی طراحی شده است. سیستم از توضیح آزاد کاربر درباره وضعیت بدنی، هدف، محدودیت‌ها، تجهیزات و سبک زندگی، یک برنامه تمرینی فارسی تولید می‌کند و دلایل تصمیم‌ها را در فایل جداگانه می‌نویسد.

## هدف خروجی

سیستم باید در پایان دو فایل Markdown فارسی تولید کند:

1. `WorkoutPlan.fa.md`
   - برنامه تمرینی نهایی برای کاربر.
   - ساده، قابل اجرا، فارسی و بدون متن فنی زیاد.

2. `DecisionReport.fa.md`
   - گزارش تصمیم‌گیری.
   - شامل داده‌های استخراج‌شده، فرضیات، ریسک‌ها، اختلاف ایجنت‌ها، قوانین اعمال‌شده و دلیل انتخاب برنامه.

## ساختار پکیج

```text
pro_fitness_multi_agent_codex/
├── README.fa.md
├── codex_master_prompt.md
├── architecture.md
├── orchestrator/
│   ├── orchestrator_prompt.md
│   └── arbitration_policy.md
├── agents/
│   ├── 01_profile_extractor.md
│   ├── 02_missing_data_challenger.md
│   ├── 03_safety_first.md
│   ├── 04_practical_continuity.md
│   ├── 05_ambitious_goal.md
│   ├── 06_realistic_goal.md
│   ├── 07_strength_hypertrophy.md
│   ├── 08_conditioning_fat_loss.md
│   ├── 09_volume_optimizer.md
│   ├── 10_recovery_protector.md
│   ├── 11_best_exercise.md
│   ├── 12_substitution_constraint.md
│   ├── 13_progressive_overload.md
│   ├── 14_fatigue_control.md
│   ├── 15_performance_nutrition.md
│   ├── 16_fat_loss_nutrition.md
│   ├── 17_discipline_coach.md
│   ├── 18_behavior_design.md
│   ├── 19_critical_reviewer.md
│   └── 20_persian_plan_writer.md
├── rules/
│   ├── safety_rules.md
│   ├── program_rules.md
│   ├── progression_rules.md
│   ├── exercise_library_contract.md
│   └── anti_hallucination_rules.md
├── schemas/
│   ├── UserFitnessProfile.schema.json
│   ├── AgentFinding.schema.json
│   ├── WorkoutPlan.schema.json
│   ├── DecisionReport.schema.json
│   └── AgentRunResult.schema.json
├── templates/
│   ├── WorkoutPlan.fa.template.md
│   └── DecisionReport.fa.template.md
└── examples/
    ├── sample_user_description.fa.md
    └── expected_output_contract.md
```

## ایده اصلی معماری

هر گروه تصمیم‌گیری دو ایجنت متضاد دارد. هدف تضاد این نیست که سیستم فقط رأی‌گیری کند؛ هدف این است که هر تصمیم مهم از دو زاویه بررسی شود. تصمیم نهایی باید با ترکیب موارد زیر گرفته شود:

- قوانین قطعی ایمنی
- دیتابیس حرکات
- محدودیت‌های پزشکی و بدنی
- سطح تمرینی فرد
- زمان و تجهیزات واقعی فرد
- داوری مرکزی Orchestrator
- گزارش قابل ردیابی تصمیم‌ها

## نکته مهم برای پیاده‌سازی

ایجنت‌ها نباید مستقیم خروجی نهایی را بسازند. هر ایجنت باید خروجی ساختاریافته بدهد. Orchestrator خروجی‌ها را جمع، تضادها را حل و سپس به Persian Plan Writer می‌دهد.

