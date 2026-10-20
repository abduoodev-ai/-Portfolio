# Smart UV-C Disinfection Robot
# روبوت التعقيم الذكي بالأشعة فوق البنفسجية UV-C

> **Status / الحالة:** Early prototype planning and integration. This repository starts with project documentation; implementation and validation are upcoming.
>
> المشروع في مرحلة تخطيط النموذج الأولي ودمج المكوّنات. يبدأ هذا المستودع بالتوثيق، وستُضاف البرمجيات ونتائج الاختبارات لاحقًا.

## العربية

### الهدف
تطوير نموذج روبوت متنقل للتعقيم باستخدام UV-C، قادر على بناء خريطة للمكان والتنقل إلى نقاط محددة داخل بيئة داخلية خالية من الأشخاص. يركز المشروع على الحركة، والاستشعار، والملاحة، والتحكم الآمن في تشغيل المصباح.

### المكوّنات التقنية الحالية
المواصفات التالية تمثل التصميم الحالي المستهدف، ولا تعني أن جميع المكوّنات قد دُمجت أو اختُبرت.

| الجزء | المواصفات |
| --- | --- |
| الحاسوب الرئيسي | Raspberry Pi 5 — ذاكرة 8 GB |
| نظام التشغيل والروبوتات | Ubuntu 24.04، ROS 2 Jazzy |
| المحاكاة والعرض | Gazebo Harmonic، RViz2 |
| البرمجة ووصف الروبوت | Python / rclpy، C++، xacro |
| الملاحة ورسم الخرائط | Nav2، slam_toolbox، robot_localization، ros_gz |
| قاعدة الحركة | دفع تفاضلي بمحركين وعجلتين وعجلة حرة؛ قطر عجلات الدفع 85 مم والعجلة الحرة 50 مم |
| المحركات ووحدة القيادة | محركان JGB37-3530 بجهد 12V مع Encoders، نسبة تخفيض 70:1 وسرعة اسمية 142 RPM؛ وحدة Cytron MDD10A |
| الاستشعار | YDLIDAR X4 PRO، كاميرا ORBBEC Astra Pro، ووحدة IMU من نوع BNO080 أو BNO085 |
| المتحكم المساعد | ESP32-S3 |
| الطاقة | بطارية LiFePO4 بجهد 12.8V وسعة 20Ah؛ منظم XL4015 بتيار اسمي 5A، مع مراجعة ملاءمة التغذية لكل جزء قبل التوصيل |
| وحدة UV-C | مصباح مستهدف بقدرة 36W وطول يقارب 900 مم؛ جهد التشغيل ودائرة القيادة لم يُحسما بعد |
| الهيكل | نموذج خشبي بكتلة مستهدفة تقارب 10 كجم؛ المحركات بالخلف والعجلة الحرة بالأمام والمصباح بالمنتصف والكاميرا أعلاه |

### نطاق المشروع
- إعداد وصف الروبوت والمحاكاة والتحكم الأساسي بالدفع التفاضلي.
- قراءة بيانات LiDAR وEncoders وIMU والكاميرا، والتحقق من الإطارات والتحويلات.
- بناء الخرائط وتحديد الموقع والتنقل إلى نقاط محددة باستخدام ROS 2.
- تصميم منطق تشغيل UV-C وحالات الإيقاف والتوثيق التجريبي.
- توثيق التوصيلات والإعدادات والاختبارات عند تنفيذها.

النموذج بحثي وتعليمي. لا يتضمن هذا النطاق ادعاء فعالية تعقيم مثبتة أو اعتمادًا طبيًا؛ قياس الجرعة والفعالية والتحقق من السلامة مراحل مستقلة قبل أي استخدام فعلي. يلزم تصميم إيقاف طوارئ وقفل أمان يمنع تشغيل UV-C عند وجود أشخاص أو حيوانات.

### المراحل القادمة
1. **التحقق من العتاد:** تأكيد مواصفات الطاقة والمصباح، اختبار المحركات والمشفّرات والحساسات كلٌّ على حدة، وتوثيق النتائج.
2. **المحاكاة:** إنشاء وصف xacro وإطارات TF ونموذج الحركة واختباره في Gazebo وRViz2.
3. **الحركة والخرائط:** دمج التحكم وقياس الحركة وLiDAR، ثم اختبار SLAM وحفظ الخرائط.
4. **الملاحة:** إعداد Nav2 واختبار تحديد الموقع وتجنب العوائق والوصول إلى النقاط.
5. **السلامة والتكامل:** تنفيذ واختبار إيقاف الطوارئ وقفل تشغيل المصباح، ثم إجراء تجارب مضبوطة وتوثيق القيود.

## English

### Goal
Develop a mobile UV-C disinfection robot prototype that maps an indoor environment and navigates to selected waypoints in spaces cleared of people. The project focuses on mobility, sensing, navigation, and safe lamp control.

### Current technical components
These specifications describe the current target design; they do not imply that every component has been integrated or tested.

| Component | Specification |
| --- | --- |
| Main computer | Raspberry Pi 5, 8 GB RAM |
| Operating system and robotics | Ubuntu 24.04, ROS 2 Jazzy |
| Simulation and visualization | Gazebo Harmonic, RViz2 |
| Programming and robot description | Python / rclpy, C++, xacro |
| Navigation and mapping | Nav2, slam_toolbox, robot_localization, ros_gz |
| Mobile base | Differential drive with two powered wheels and one caster; 85 mm drive wheels and a 50 mm caster |
| Motors and driver | Two JGB37-3530 12V encoder motors, 70:1 reduction, nominal 142 RPM; Cytron MDD10A |
| Sensors | YDLIDAR X4 PRO, ORBBEC Astra Pro camera, BNO080 or BNO085 IMU |
| Auxiliary controller | ESP32-S3 |
| Power | 12.8V 20Ah LiFePO4 battery; XL4015 regulator rated at 5A, with power suitability to be checked for each load before wiring |
| UV-C unit | Target 36W lamp, approximately 900 mm long; operating voltage and driver circuit remain to be confirmed |
| Chassis | Wooden prototype targeting approximately 10 kg; rear motors, front caster, central lamp, and camera above the lamp |

### Scope
- Robot description, simulation, and basic differential-drive control.
- LiDAR, encoder, IMU, and camera integration, including frame and transform verification.
- Mapping, localization, and waypoint navigation using ROS 2.
- UV-C control logic, shutdown behavior, and experimental documentation.
- Wiring, configuration, and test documentation as implementation progresses.

This is a research and educational prototype. Proven disinfection efficacy and medical certification are outside this initial scope; dose measurement, efficacy validation, and safety verification are separate requirements before real use. Emergency-stop and safety-interlock mechanisms must prevent UV-C operation around people or animals.

### Next milestones
1. **Hardware verification:** Confirm power and lamp specifications, test motors, encoders, and sensors individually, and record results.
2. **Simulation:** Build the xacro description, TF frames, and drive model; verify them in Gazebo and RViz2.
3. **Motion and mapping:** Integrate drive control, odometry, and LiDAR; test SLAM and save maps.
4. **Navigation:** Configure Nav2; test localization, obstacle avoidance, and waypoint arrival.
5. **Safety and integration:** Implement and test emergency-stop and lamp interlocks, then run controlled experiments and document limitations.
