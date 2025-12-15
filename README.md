<!doctype html>
<html lang="vi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Quiz Vi Sinh Vật Đại Cương</title>
  <style>
    :root{
      --bg:#fffef6; --card:#E6F8F9; --accent:#00b894; --accent-2:#0984e3; --danger:#f81a02; --ok:#0ed630; --muted:#6b6b6b; --glass: rgba(255,255,255,0.7);
      --radius:16px; --pad:16px; --btn-h:56px; --shadow:0 8px 20px rgba(0, 0, 0, 0.08);
    }
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial; background:linear-gradient(180deg,#f7fff9 0%, #fff 100%); color:#111}
    .app{max-width:900px;margin:18px auto;padding:16px}
    header{display:flex;align-items:center;gap:12px}
    .logo{width:56px;height:56px;border-radius:12px;background:linear-gradient(135deg,var(--accent),var(--accent-2));display:flex;align-items:center;justify-content:center;color:white;font-weight:700;font-size:20px;box-shadow:var(--shadow)}
    h1{font-size:18px;margin:0}
    .sub{color:var(--muted);font-size:13px}

    .card{background:var(--card);border-radius:var(--radius);padding:var(--pad);box-shadow:var(--shadow);margin-top:12px}
    .question{font-size:18px;font-weight:600;min-height:68px}
    .meta{display:flex;justify-content:space-between;align-items:center;margin-top:8px}
    .progress{font-size:13px;color:var(--muted)}
    .answers{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:12px}
    .btn-answer{background:var(--glass);border-radius:12px;padding:12px;min-height:54px;display:flex;align-items:center;gap:10px;border:2px solid transparent;cursor:pointer;transition:transform .12s ease, box-shadow .12s ease, border-color .12s ease;box-shadow:0 6px 14px rgba(10,10,20,0.05);}    
    .btn-answer:active{transform:translateY(1px)}
    .btn-answer .label{font-weight:700;width:28px;height:28px;border-radius:8px;display:inline-flex;align-items:center;justify-content:center;background:rgba(0,0,0,0.06)}
    .btn-answer .text{flex:1}

    .btn-answer.correct{background:linear-gradient(90deg,#eaffef,#f3fff7);border-color:rgba(46,204,113,0.18)}
    .btn-answer.wrong{background:linear-gradient(90deg,#fff5f6,#fffafb);border-color:rgba(231,76,60,0.12)}
    .btn-answer.correct .label{background:var(--ok);color:white}
    .btn-answer.wrong .label{background:var(--danger);color:white}
    .btn-answer.correct .text, .btn-answer.wrong .text{font-weight:700}

    .explain{margin-top:12px;padding:12px;border-radius:10px;background:#fbfdff;border:1px solid rgba(8,65,138,0.03);min-height:48px;color:#123}
    .controls{display:flex;gap:10px;margin-top:12px}
    .btn{flex:1;min-height:var(--btn-h);border-radius:12px;border:0;font-weight:700;cursor:pointer;box-shadow:var(--shadow);}
    .btn.ghost{background:transparent;border:1px solid rgba(0,0,0,0.06)}
    .btn.primary{background:linear-gradient(90deg,var(--accent),var(--accent-2));color:white}
    .btn.secondary{background:linear-gradient(90deg,#ffd166,#ff8aac);color:#2b2b2b}

    footer{margin-top:18px;text-align:center;color:var(--muted);font-size:13px}
    .small{font-size:12px;color:var(--muted)}

    /* Responsive */
    @media (max-width:520px){
      .answers{grid-template-columns:1fr}
      .logo{width:48px;height:48px}
      h1{font-size:16px}
    }

    /* Little animations */
    .fade-in{animation:fadeIn .28s ease both}
    @keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}

    /* make buttons fixed height even if text wraps */
    .btn-answer .text{max-height:56px;overflow:hidden}
  </style>
</head>
<body>
  <div class="app">
    <header>
      <div class="logo">Quiz</div>
      <div>
        <h1>Quiz Vi Sinh Vật Đại Cương - VNUA </h1>
        <div class="sub">© by Viet K70TYB</div>
      </div>
    </header>

    <div class="card">
      <div class="meta">
        <div class="progress" id="progress">Câu 1 / 1</div>
        <div class="progress" id="score">Điểm: 0</div>
      </div>

      <div class="question fade-in" id="question">Đang tải câu hỏi…</div>

      <div class="answers" id="answers">
        <!-- buttons inserted by JS -->
      </div>

      <div class="explain" id="explain" aria-live="polite">Chọn đáp án để xem kết quả và lời giải.</div>

      <div class="controls">
        <button class="btn ghost" id="restart">Làm lại</button>
        <button class="btn" id="prev">Quay lại</button>
        <button class="btn primary" id="next">Câu tiếp theo</button>
      </div>
    </div>

    <footer>
      <div class="small">Cố gắng lấy điểm 200 nha^^  <span id="local-info"></span></div>
    </footer>
  </div>

  <script>
    // ---------- configuration ----------
    const STORAGE_KEY = 'via_quiz_state_v2';
    const SNAPSHOT_KEY = 'via_quiz_snapshot_v2'; // used to persist the working (shuffled) questions when saving progress
    const QUESTIONS_PATH = 'questions.json'; // optional external file

    // ---------- embedded fallback questions ----------
    const embeddedQuestions = [
      

   /*chương 2*/

    {
  id: 1,
  q: "Đặc điểm nổi bật nhất để phân biệt vi khuẩn với sinh vật nhân thực là gì?",
  choices: [
    "Có kích thước lớn và cấu tạo phức tạp",
    "Có nhiều bào quan có màng",
    "Là sinh vật nhân sơ, không có nhân thật và không có màng nhân",
    "Có hệ thống nội màng phát triển"
  ],
  answer: 2,
  explain: "Vi khuẩn thuộc nhóm sinh vật nhân sơ (prokaryote), đặc trưng bởi việc không có nhân thật và không có màng nhân, khác hoàn toàn với sinh vật nhân thực vốn có màng bao nhân và nhiều bào quan màng."
},
{
  id: 2,
  q: "Kích thước điển hình của vi khuẩn thường nằm trong khoảng nào?",
  choices: [
    "50–100 µm",
    "0,2–10 µm",
    "0,01–0,1 µm",
    "20–40 µm"
  ],
  answer: 1,
  explain: "Vi khuẩn có kích thước nhỏ, thường 1–10 µm, và chiều ngang từ 0,2–10 µm, cho phép chúng phân chia nhanh và thích nghi tốt với nhiều môi trường."
},
{
  id: 3,
  q: "Cấu tạo cơ bản của tế bào vi khuẩn bao gồm những thành phần nào?",
  choices: [
    "Nhân thật – ti thể – mạng nội chất",
    "Chỉ có vách tế bào và nhân",
    "Vách tế bào, màng tế bào, tế bào chất và thể nhân (ADN vòng)",
    "Lục lạp – bộ máy Golgi – ti thể"
  ],
  answer: 2,
  explain: "Vi khuẩn có cấu tạo đơn giản gồm vách tế bào, màng tế bào, tế bào chất, và thể nhân chứa ADN dạng vòng. Chúng không có các bào quan có màng như ti thể hay lục lạp."
},
{
  id: 4,
  q: "Cấu trúc nào ở vi khuẩn giúp chúng di động trong môi trường?",
  choices: [
    "Không bào",
    "Ti thể",
    "Tiên mao hoặc lông",
    "Lục lạp"
  ],
  answer: 2,
  explain: "Một số vi khuẩn có tiên mao (flagella) hoặc lông (fimbriae) giúp chúng di chuyển hoặc bám vào bề mặt. Đây là đặc điểm quan trọng giúp vi khuẩn thích nghi và gây bệnh."
},
{
  id: 5,
  q: "Vi khuẩn tạo vỏ nhầy hoặc nha bào chủ yếu nhằm mục đích gì?",
  choices: [
    "Tăng tốc độ sinh sản",
    "Tăng khả năng quang hợp",
    "Tồn tại trong điều kiện bất lợi của môi trường",
    "Tăng khả năng chuyển hóa đường"
  ],
  answer: 2,
  explain: "Vỏ nhầy giúp vi khuẩn tránh thực bào, còn nha bào giúp vi khuẩn sống sót trong điều kiện khắc nghiệt như nhiệt độ cao, khô hạn, hóa chất… Đây là cơ chế bảo vệ quan trọng của vi khuẩn."
},
{
  id: 6,
  q: "Vi khuẩn sinh sản chủ yếu bằng hình thức nào?",
  choices: [
    "Nảy chồi",
    "Thụ tinh",
    "Phân đôi (sinh sản vô tính)",
    "Tạo giao tử"
  ],
  answer: 2,
  explain: "Vi khuẩn sinh sản rất nhanh nhờ hình thức phân đôi, giúp số lượng tăng theo cấp số nhân. Dù là vô tính nhưng chúng có thể trao đổi vật liệu di truyền qua tiếp hợp, biến nạp, tải nạp để tăng đa dạng di truyền."
},

{
  id: 7,
  q: "Dạng cầu khuẩn nào gồm các tế bào đứng riêng rẽ, không tạo đôi hay chuỗi?",
  choices: [
    "Tụ cầu khuẩn",
    "Song cầu khuẩn",
    "Vi cầu khuẩn (Micrococcus/Monococcus)",
    "Bát cầu khuẩn"
  ],
  answer: 2,
  explain: "Vi cầu khuẩn tồn tại từng tế bào riêng lẻ, không kết cặp hay thành chuỗi. Chúng thường sống hoại sinh trong đất, nước, không khí."
},
{
  id: 8,
  q: "Dạng cầu khuẩn nào có tế bào chia theo một mặt phẳng và dính thành từng đôi?",
  choices: [
    "Liên cầu khuẩn",
    "Song cầu khuẩn (Diplococcus)",
    "Sarcina",
    "Tụ cầu khuẩn"
  ],
  answer: 1,
  explain: "Song cầu khuẩn phân chia theo một mặt phẳng, sau đó hai tế bào dính thành từng đôi – đây là đặc điểm hình thái tiêu biểu của Diplococcus."
},
{
  id: 9,
  q: "Dạng cầu khuẩn nào được tạo thành do phân chia theo hai mặt phẳng vuông góc, tạo nhóm 4 tế bào?",
  choices: [
    "Liên cầu khuẩn",
    "Vi cầu khuẩn",
    "Tứ cầu khuẩn (Tetracoccus)",
    "Tụ cầu khuẩn"
  ],
  answer: 2,
  explain: "Tứ cầu khuẩn hình thành nhờ sự phân chia theo hai mặt phẳng vuông góc, tạo thành nhóm 4 tế bào — đặc trưng của Tetracoccus."
},
{
  id: 10,
  q: "Bát cầu khuẩn (Sarcina) phân chia theo đặc điểm nào?",
  choices: [
    "Chia theo nhiều mặt phẳng tạo đám giống chùm nho",
    "Chia theo hai mặt phẳng tạo 4 tế bào",
    "Chia theo ba mặt phẳng vuông góc, tạo khối 8 hoặc 16 tế bào",
    "Chia theo một mặt phẳng tạo đôi tế bào"
  ],
  answer: 2,
  explain: "Sarcina phân chia theo ba mặt phẳng vuông góc, tạo thành khối 8 hoặc 16 tế bào, thường sống hoại sinh và có khả năng phân giải ure mạnh."
},
{
  id: 11,
  q: "Dạng cầu khuẩn nào tạo thành các chuỗi dài khi tế bào chia theo một mặt phẳng nhưng vẫn dính nhau?",
  choices: [
    "Tụ cầu khuẩn",
    "Liên cầu khuẩn (Streptococcus)",
    "Sarcina",
    "Tứ cầu khuẩn"
  ],
  answer: 1,
  explain: "Liên cầu khuẩn phân chia theo một mặt phẳng, nhưng các tế bào gắn kết thành chuỗi dài. Độ dài chuỗi phụ thuộc vào môi trường nuôi cấy."
},
{
  id: 12,
  q: "Dạng cầu khuẩn nào phân chia theo nhiều mặt phẳng khác nhau và tạo thành đám giống chùm nho?",
  choices: [
    "Song cầu khuẩn",
    "Vi cầu khuẩn",
    "Tụ cầu khuẩn (Staphylococcus)",
    "Tứ cầu khuẩn"
  ],
  answer: 2,
  explain: "Tụ cầu khuẩn phân chia theo nhiều mặt phẳng, tạo thành đám tế bào giống chùm nho, là đặc điểm điển hình của chi Staphylococcus."
},

{
  id: 13,
  q: "Trực khuẩn nói chung có hình dạng như thế nào?",
  choices: [
    "Hình cầu tạo chuỗi",
    "Hình xoắn",
    "Hình que hoặc hình gậy",
    "Hình tam giác"
  ],
  answer: 2,
  explain: "Trực khuẩn là vi khuẩn hình que/hình gậy, kích thước phổ biến khoảng 0,5–1 × 1–4 µm. Đây là dạng hình thái điển hình của nhiều vi khuẩn quan trọng."
},
{
  id: 14,
  q: "Đặc điểm nào đúng với chi Bacillus?",
  choices: [
    "Gram âm, không sinh nha bào",
    "Gram dương, hiếu khí, có sinh nha bào nhỏ hơn thân",
    "Gram dương, kỵ khí, nha bào làm phình tế bào",
    "Gram âm, hiếu khí, không lông"
  ],
  answer: 1,
  explain: "Bacillus là Gram dương, sống hiếu khí, và có sinh nha bào. Nha bào của chúng nhỏ hơn thân nên không làm biến dạng tế bào, giúp phân biệt với Clostridium."
},
{
  id: 15,
  q: "Clostridium có đặc điểm hình thái nào nổi bật?",
  choices: [
    "Không sinh nha bào",
    "Gram âm, có lông xung quanh thân",
    "Gram dương, yếm khí, nha bào to làm tế bào biến dạng như hình trống",
    "Gram dương nhưng nha bào nhỏ, không làm biến dạng tế bào"
  ],
  answer: 2,
  explain: "Clostridium là Gram dương, kỵ khí, và có nha bào rất to làm tế bào phình ra thành hình trống hoặc đinh ghim, là đặc điểm nhận dạng quan trọng."
},
{
  id: 16,
  q: "Dạng trực khuẩn nào thuộc nhóm Gram âm và không sinh nha bào?",
  choices: [
    "Bacillus",
    "Clostridium",
    "Bacterium",
    "Corynebacterium"
  ],
  answer: 2,
  explain: "Bacterium là Gram âm, không sinh nha bào, và thường có lông xung quanh thân, giúp chúng di động và bám dính tốt."
},
{
  id: 17,
  q: "Trực khuẩn Gram dương, hiếu khí tùy tiện, không có lông là đặc điểm của nhóm nào?",
  choices: [
    "Corynebacterium",
    "Bacillus",
    "Clostridium",
    "Bacterium"
  ],
  answer: 0,
  explain: "Corynebacterium là trực khuẩn Gram dương, hiếu khí tùy tiện, và không có lông. Chúng thường có hình dạng hơi phình và xếp kiểu chữ H, L hoặc V."
},
{
  id: 18,
  q: "Điểm nào giúp phân biệt Bacillus và Clostridium?",
  choices: [
    "Bacillus không sinh nha bào còn Clostridium sinh nha bào",
    "Bacillus Gram âm còn Clostridium Gram dương",
    "Bacillus hiếu khí, nha bào nhỏ; Clostridium yếm khí, nha bào to làm biến dạng tế bào",
    "Bacillus có lông còn Clostridium không có lông"
  ],
  answer: 2,
  explain: "Bacillus là hiếu khí và có nha bào nhỏ, không làm biến dạng tế bào; trong khi Clostridium là kỵ khí và có nha bào lớn làm phình tế bào thành hình trống hoặc đinh ghim."
},


{
  id: 19,
  q: "Cầu trực khuẩn (Coccobacterium) có hình dạng đặc trưng như thế nào?",
  choices: [
    "Hình que cong giống dấu phẩy",
    "Hình xoắn đều, nhiều vòng",
    "Hình trứng hoặc bầu dục",
    "Hình cầu đứng riêng rẽ"
  ],
  answer: 2,
  explain: "Cầu trực khuẩn là dạng trung gian giữa cầu khuẩn và trực khuẩn, vì vậy chúng có hình trứng hoặc bầu dục, kích thước nhỏ (0,25–0,4 × 0,4–1,5 µm)."
},
{
  id: 20,
  q: "Đặc điểm nhuộm Gram của cầu trực khuẩn (Coccobacterium) là gì?",
  choices: [
    "Gram dương, bắt màu tím mạnh",
    "Gram âm, bắt màu hồng",
    "Không nhuộm được Gram",
    "Gram dương nhưng phải nhuộm bạc"
  ],
  answer: 1,
  explain: "Cầu trực khuẩn bắt màu Gram âm (–), vì vậy trong nhuộm Gram sẽ hiện màu hồng, phù hợp cấu trúc vách tế bào mỏng."
},
{
  id: 21,
  q: "Xoắn khuẩn (Spirillum) được đặc trưng bởi điều nào sau đây?",
  choices: [
    "Có một vòng xoắn duy nhất",
    "Không có khả năng di động",
    "Có từ hai vòng xoắn trở lên",
    "Chỉ sống hoại sinh"
  ],
  answer: 2,
  explain: "Xoắn khuẩn thuộc nhóm vi khuẩn có từ hai vòng xoắn trở lên. Chúng di động nhờ sự co rút của thân, tạo nên chuyển động đặc trưng."
},
{
  id: 22,
  q: "Loài xoắn khuẩn Treponema có kiểu xoắn như thế nào?",
  choices: [
    "Vòng xoắn nhỏ, hai đầu cong móc câu",
    "Vòng xoắn thưa, không đều",
    "Nhiều vòng xoắn đều và sát nhau",
    "Không có vòng xoắn, chỉ cong nhẹ"
  ],
  answer: 2,
  explain: "Treponema (gây bệnh giang mai) có nhiều vòng xoắn đều, sát nhau, giúp tăng tính linh hoạt và khả năng di động."
},
{
  id: 23,
  q: "Đặc điểm nào đúng với Leptospira?",
  choices: [
    "Có nhiều vòng xoắn thưa",
    "Vòng xoắn nhỏ, hai đầu cong hình móc câu",
    "Không di động",
    "Có hình dấu phẩy"
  ],
  answer: 1,
  explain: "Leptospira có vòng xoắn nhỏ, và hai đầu cong như móc câu, là đặc điểm đặc trưng giúp nhận diện nhóm này trong kính hiển vi nền đen."
},
{
  id: 24,
  q: "Đặc điểm nổi bật của phảy khuẩn (Vibrio) là gì?",
  choices: [
    "Hình cầu nhỏ, không di động",
    "Hình que cong giống dấu phẩy, có lông và di động mạnh",
    "Hình xoắn đều nhiều vòng",
    "Hình trứng bắt Gram âm yếu"
  ],
  answer: 1,
  explain: "Phảy khuẩn Vibrio có hình cong giống dấu phẩy “,”, thường có 1 lông ở đầu, di động mạnh. Một số loài gây bệnh như Vibrio cholerae."
},

{
  id: 25,
  q: "Tế bào vi khuẩn gồm ba phần chính nào sau đây?",
  choices: [
    "Màng tế bào – nguyên sinh chất – thể nhân",
    "Nhân thật – ty thể – màng tế bào",
    "Màng sinh chất – lục lạp – ribosom 80S",
    "Vỏ – nhân con – bào quan màng"
  ],
  answer: 0,
  explain: "Tế bào vi khuẩn có cấu tạo đơn giản với 3 phần cơ bản: màng tế bào, nguyên sinh chất, và thể nhân (nucleoid không có màng nhân)."
},
{
  id: 26,
  q: "Thành phần nào của tế bào vi khuẩn chứa peptidoglycan?",
  choices: [
    "Màng sinh chất",
    "Thành tế bào",
    "Lông (fimbriae)",
    "Nha bào"
  ],
  answer: 1,
  explain: "Thành tế bào vi khuẩn được cấu tạo chủ yếu từ peptidoglycan, quyết định tính chất Gram dương – Gram âm."
},
{
  id: 27,
  q: "Ribosom của vi khuẩn thuộc loại nào?",
  choices: [
    "80S",
    "50S",
    "70S",
    "90S"
  ],
  answer: 2,
  explain: "Vi khuẩn sử dụng ribosom 70S; đây là đích tác động của nhiều loại kháng sinh ức chế tổng hợp protein."
},
{
  id: 28,
  q: "ADN trong thể nhân (nucleoid) của vi khuẩn có đặc điểm gì?",
  choices: [
    "ADN kép dạng vòng",
    "ADN nằm trong nhân thật",
    "ADN đơn mạch tự nhân đôi",
    "Không có cấu trúc di truyền"
  ],
  answer: 0,
  explain: "ADN của vi khuẩn là ADN kép dạng vòng, không có màng nhân bao bọc. Vi khuẩn còn có thể sở hữu plasmid mang gen phụ."
},
{
  id: 29,
  q: "Cấu trúc nào của vi khuẩn có chức năng giúp di động?",
  choices: [
    "Lông (fimbriae)",
    "Capsule",
    "Tiêm mao (flagella)",
    "Plasmid"
  ],
  answer: 2,
  explain: "Tiêm mao (flagella) giúp vi khuẩn di động, tùy loài có thể có một, nhiều hoặc phân bố xung quanh tế bào."
},
{
  id: 30,
  q: "Capsule có vai trò gì đối với vi khuẩn?",
  choices: [
    "Giúp chống thực bào, tăng độc lực",
    "Giúp tổng hợp protein",
    "Giúp sinh sản nhanh hơn",
    "Giúp vận chuyển chất qua màng"
  ],
  answer: 0,
  explain: "Capsule giúp vi khuẩn tránh bị thực bào, từ đó tăng độc lực, đặc biệt ở các loài như Klebsiella và Streptococcus pneumoniae."
},

{
  id: 31,
  q: "Giáp mô của vi khuẩn nằm ở đâu?",
  choices: [
    "Nằm bên ngoài thành tế bào, bao quanh toàn bộ tế bào vi khuẩn",
    "Xen giữa màng sinh chất và peptidoglycan",
    "Nằm trong nguyên sinh chất",
    "Chỉ có ở vi khuẩn Gram dương"
  ],
  answer: 0,
  explain: "Giáp mô (capsule) là lớp ngoài cùng bao bọc vi khuẩn, tạo thành lớp nhầy bảo vệ và tăng độc lực."
},
{
  id: 32,
  q: "Thành phần cấu tạo chính của giáp mô là gì?",
  choices: [
    "Protein và lipid",
    "Polysaccharide chứa tới 98% nước",
    "DNA và RNA",
    "Peptidoglycan dạng sợi dày"
  ],
  answer: 1,
  explain: "Capsule chủ yếu gồm polysaccharide và giàu nước (~98%), tạo cấu trúc mềm – nhầy đặc trưng."
},
{
  id: 33,
  q: "Đặc điểm cấu trúc nào mô tả đúng giáp mô?",
  choices: [
    "Mềm, nhầy, dễ biến dạng",
    "Cứng, khó thay đổi hình dạng",
    "Chỉ gồm lipid khô",
    "Có dạng tinh thể"
  ],
  answer: 0,
  explain: "Giáp mô là lớp nhầy mềm, đàn hồi, thay đổi độ dày tùy loài."
},
{
  id: 34,
  q: "Giáp mô có vai trò quan trọng nhất trong việc tăng độc lực là:",
  choices: [
    "Tăng tốc độ phân chia tế bào",
    "Chống lại thực bào của ký chủ",
    "Giảm tiêu thụ chất dinh dưỡng",
    "Tăng khả năng quang hợp"
  ],
  answer: 1,
  explain: "Capsule ngăn bạch cầu thực bào, giúp vi khuẩn tồn tại lâu hơn trong cơ thể và trở nên độc lực hơn."
},
{
  id: 35,
  q: "Giáp mô giúp vi khuẩn chống lại yếu tố bất lợi nào sau đây?",
  choices: [
    "Ánh sáng mạnh",
    "Khô hạn và tác động cơ học",
    "Áp suất thẩm thấu thấp",
    "Nhiệt độ cao kéo dài"
  ],
  answer: 1,
  explain: "Capsule chứa nhiều nước, ngăn mất nước, đồng thời giảm tổn thương do tác động cơ học hay hóa chất."
},
{
  id: 36,
  q: "Chức năng nào KHÔNG thuộc về giáp mô?",
  choices: [
    "Bảo vệ chống enzyme tiêu hóa",
    "Tạo năng lượng cho tế bào",
    "Tăng khả năng bám dính",
    "Tích lũy chất dinh dưỡng"
  ],
  answer: 1,
  explain: "Giáp mô không tham gia chuyển hóa hay sinh năng lượng; đây là chức năng nội bào."
},
{
  id: 37,
  q: "Giáp mô đóng vai trò quan trọng trong:",
  choices: [
    "Bám dính lên mô và bề mặt",
    "Tổng hợp ribosom",
    "Tạo lông bám ở bề mặt tế bào",
    "Điều chỉnh hoạt động enzyme nội bào"
  ],
  answer: 0,
  explain: "Capsule hỗ trợ bám dính vào mô, thiết bị y tế… là bước đầu hình thành biofilm."
},
{
  id: 38,
  q: "Trong thành phần giáp mô, nước chiếm khoảng bao nhiêu?",
  choices: [
    "98%",
    "40%",
    "12%",
    "5%"
  ],
  answer: 0,
  explain: "Giáp mô rất giàu nước (≈98%), lý giải tính mềm – nhầy và chức năng giữ ẩm rất tốt."
},
{
  id: 39,
  q: "Giáp mô giúp bảo vệ vi khuẩn khỏi loại enzyme nào của ký chủ?",
  choices: [
    "Amylase",
    "Pepsin",
    "Các enzyme tiêu hóa của ký chủ (ví dụ lysozyme)",
    "Catalase"
  ],
  answer: 2,
  explain: "Capsule hạn chế tác động của enzyme tiêu hóa từ hệ miễn dịch, hỗ trợ vi khuẩn tồn tại."
},
{
  id: 40,
  q: "Vi khuẩn nào sau đây là ví dụ điển hình có giáp mô làm tăng độc lực?",
  choices: [
    "Vibrio parahaemolyticus",
    "Escherichia coli",
    "Treponema pallidum",
    "Bacillus anthracis"
  ],
  answer: 3,
  explain: "Bacillus anthracis có capsule đặc trưng giúp chống thực bào, là yếu tố chính tạo độc lực."
},

{
  id: 41,
  q: "Nha bào có sức đề kháng như thế nào?",
  choices: [
    "Chịu được đun sôi nhiều giờ, tia UV, hóa chất sát trùng, khô hạn và thay đổi áp suất thẩm thấu",
    "Chỉ tồn tại được vài giờ ngoài môi trường",
    "Rất nhạy cảm với bức xạ và nhiệt độ",
    "Dễ bị phá hủy bởi các chất sát khuẩn thông thường"
  ],
  answer: 0,
  explain: "Nha bào có thể chịu nhiệt, tia UV, hóa chất, khô hạn và tồn tại hàng chục năm. Đây là dạng đề kháng cao nhất của vi khuẩn."
},
{
  id: 42,
  q: "Yếu tố nào giúp nha bào chịu nhiệt tốt?",
  choices: [
    "Có nhiều túi khí cách nhiệt",
    "Nước trong nha bào ở trạng thái liên kết, không tự do",
    "Hàm lượng lipid cao",
    "Có enzyme chống nóng hoạt động mạnh"
  ],
  answer: 1,
  explain: "Nước liên kết làm protein không bị biến tính dưới nhiệt độ cao → tăng khả năng chịu nhiệt."
},
{
  id: 43,
  q: "Chất nào trong nha bào kết hợp với Ca²⁺ tạo phức bền vững giúp đề kháng cao?",
  choices: [
    "Acid lactic",
    "Acid citric",
    "Acid dipicolinic",
    "Acid acetic"
  ],
  answer: 2,
  explain: "Phức calcium–dipicolinate đặc trưng cho nha bào → rất bền nhiệt và bền hóa chất."
},
{
  id: 44,
  q: "Lý do nha bào khó bị hóa chất sát trùng xâm nhập là gì?",
  choices: [
    "Nha bào có lớp nhầy dày bao quanh",
    "Có khả năng tiết kháng sinh",
    "Có enzyme phân hủy hóa chất",
    "Có nhiều lớp màng bao bọc với tính thấm kém"
  ],
  answer: 3,
  explain: "Nhiều lớp màng lipid–protein xếp chặt → hóa chất khó xuyên qua → tăng đề kháng."
},
{
  id: 45,
  q: "Đặc điểm nào giúp nha bào chịu được khô hạn và tác động cơ học?",
  choices: [
    "Cấu trúc đặc, ít nước",
    "Có lông bám dày",
    "Có hệ enzyme hoạt động mạnh",
    "Có màng chứa dịch nhầy tự tái tạo"
  ],
  answer: 0,
  explain: "Nha bào chứa rất ít nước → hạn chế mất nước → bền với khô hạn và tác động cơ học."
},

{
  id: 46,
  q: "Đặc điểm hình thái nổi bật nhất của xạ khuẩn là gì?",
  choices: [
    "Có dạng sợi phân nhánh giống nấm mốc",
    "Có dạng cầu, đứng thành cụm",
    "Có dạng que ngắn",
    "Có dạng xoắn nhiều vòng"
  ],
  answer: 0,
  explain: "Xạ khuẩn phát triển dạng sợi phân nhánh, rất giống nấm mốc – đây là điểm phân biệt chính."
},
{
  id: 47,
  q: "Trên môi trường đặc, khuẩn ty nào của xạ khuẩn cắm sâu vào môi trường để hút dinh dưỡng?",
  choices: [
    "Khuẩn ty khí sinh",
    "Khuẩn ty cơ chất",
    "Khuẩn ty ngoại bào",
    "Khuẩn ty trung tâm"
  ],
  answer: 1,
  explain: "Khuẩn ty cơ chất (substrate mycelium) bám sâu xuống môi trường để hấp thu chất dinh dưỡng."
},
{
  id: 48,
  q: "Đường kính của sợi xạ khuẩn thường nằm trong khoảng bao nhiêu?",
  choices: [
    "2–4 µm",
    "3–8 µm",
    "0,2 – 1,5 µm",
    "10–15 µm"
  ],
  answer: 2,
  explain: "Xạ khuẩn có sợi rất nhỏ, chỉ từ 0,2–1,5 µm, bắt màu Gram dương."
},
{
  id: 49,
  q: "Đặc điểm đúng về xạ khuẩn khi chúng già là:",
  choices: [
    "Tách thành tế bào riêng biệt",
    "Biến đổi thành dạng cầu",
    "Tạo enzyme phân giải mạnh",
    "Dễ gãy thành từng đoạn nhỏ"
  ],
  answer: 3,
  explain: "Khuẩn ty già rất giòn và thường gãy thành các đoạn ngắn."
},
{
  id: 50,
  q: "Trên môi trường lỏng, xạ khuẩn thường có dạng gì?",
  choices: [
    "Dạng sợi bông",
    "Dạng khuẩn lạc trơn nhẵn",
    "Dạng lắng thành hạt",
    "Dạng vi cầu"
  ],
  answer: 0,
  explain: "Xạ khuẩn trong môi trường lỏng tạo thành các khối sợi bông đặc trưng."
},
{
  id: 51,
  q: "Một vai trò quan trọng của xạ khuẩn trong tự nhiên là gì?",
  choices: [
    "Gây lên men rượu",
    "Phân hủy chất hữu cơ, làm giàu độ phì của đất",
    "Tạo bào tử độc tố",
    "Tạo mucopolysaccharide"
  ],
  answer: 1,
  explain: "Xạ khuẩn phân giải chất hữu cơ và góp phần cải thiện độ phì nhiêu của đất."
},
{
  id: 52,
  q: "Trong công nghiệp, xạ khuẩn được dùng rộng rãi để sản xuất:",
  choices: [
    "Kháng nguyên và độc tố",
    "Hormone tăng trưởng",
    "Enzyme, vitamin nhóm B, acid hữu cơ",
    "Lệch tâm protein"
  ],
  answer: 2,
  explain: "Xạ khuẩn rất quan trọng trong công nghiệp lên men → tạo enzyme, vitamin B, acid lactic, acetic…"
},
{
  id: 53,
  q: "Khoảng bao nhiêu phần trăm xạ khuẩn có khả năng sinh kháng sinh?",
  choices: [
    "10%",
    "25%",
    "50%",
    "70%"
  ],
  answer: 3,
  explain: "70% các chủng xạ khuẩn phân lập được có khả năng tạo kháng sinh → vai trò y học rất lớn."
},
{
  id: 54,
  q: "Một số loài xạ khuẩn gây bệnh gì cho người và động vật?",
  choices: [
    "Nhiễm trùng huyết",
    "Actinomycosis",
    "Lao phổi",
    "Viêm ruột hoại tử"
  ],
  answer: 1,
  explain: "Một số xạ khuẩn gây bệnh dạng Actinomycosis – khó điều trị."
},
{
  id: 55,
  q: "Đặc điểm khuẩn lạc xạ khuẩn thường gặp trên môi trường đặc là:",
  choices: [
    "Rắn, thô ráp, nhiều màu sắc",
    "Trong suốt như giáp mô",
    "Màu đen đồng nhất",
    "Mềm và nhầy như vibrio"
  ],
  answer: 0,
  explain: "Khuẩn lạc xạ khuẩn thường rắn, sần sùi và có nhiều màu sắc (trắng, đỏ, vàng, xanh, hồng…)."
},

{
  id: 56,
  q: "Nấm mốc thuộc nhóm vi sinh vật nào?",
  choices: [
    "Vi sinh vật nhân thực, đa bào dạng sợi",
    "Vi sinh vật nhân sơ, dạng que",
    "Vi sinh vật đơn bào có roi",
    "Vi sinh vật ký sinh nội bào"
  ],
  answer: 0,
  explain: "Nấm mốc là sinh vật nhân thực (eukaryote) và phát triển dạng sợi."
},
{
  id: 57,
  q: "Các sợi nấm mốc tập hợp lại tạo thành cấu trúc gì?",
  choices: [
    "Túi bào tử",
    "Tản nấm (khuẩn lạc)",
    "Chùm roi",
    "Tiêm mao"
  ],
  answer: 1,
  explain: "Khuẩn ty nấm mốc kết hợp tạo thành tản nấm thường có màu đặc trưng."
},
{
  id: 58,
  q: "Nấm mốc sinh sản bằng cơ chế nào?",
  choices: [
    "Phân đôi đơn giản",
    "Tạo bào tử trên cuống bào tử",
    "Tạo nang nguyên sinh",
    "Tách chồi"
  ],
  answer: 1,
  explain: "Nấm mốc sinh sản bằng bào tử, thường nằm trên các cuống bào tử như conidiophore."
},
{
  id: 59,
  q: "Khuẩn lạc nấm mốc trên môi trường đặc thường có đặc điểm gì?",
  choices: [
    "Mịn, bóng, không màu",
    "Nhầy và trong",
    "Bông, xốp, nhiều màu sắc",
    "Kết tinh như muối"
  ],
  answer: 2,
  explain: "Nấm mốc phát triển thành khuẩn lạc bông, xốp, có thể màu xanh, vàng, đen…"
},
{
  id: 60,
  q: "Một vai trò quan trọng của nấm mốc trong tự nhiên là:",
  choices: [
    "Tăng tốc độ oxy hóa kim loại",
    "Phân hủy chất hữu cơ tạo mùn",
    "Làm giảm độ pH đất đột ngột",
    "Sản xuất polysaccharide ngoại bào"
  ],
  answer: 1,
  explain: "Nấm mốc giúp phân hủy chất hữu cơ → góp phần tạo mùn cho đất."
},
{
  id: 61,
  q: "Nấm mốc được ứng dụng để sản xuất acid hữu cơ nào sau đây?",
  choices: [
    "Acid oxalic",
    "Acid citric",
    "Acid chloric",
    "Acid uric"
  ],
  answer: 1,
  explain: "Aspergillus niger được dùng nhiều để sản xuất acid citric."
},
{
  id: 62,
  q: "Loài nấm mốc nào nổi tiếng trong sản xuất kháng sinh penicillin?",
  choices: [
    "Aspergillus flavus",
    "Rhizopus oligosporus",
    "Penicillium chrysogenum",
    "Mucor rouxii"
  ],
  answer: 2,
  explain: "Penicillium tạo ra penicillin – kháng sinh đầu tiên."
},
{
  id: 63,
  q: "Tác hại thường gặp của nấm mốc đối với thực phẩm là gì?",
  choices: [
    "Tạo lớp bảo vệ chống oxy hóa",
    "Làm khô nhanh thực phẩm",
    "Gây hỏng thực phẩm giàu tinh bột và đường",
    "Làm giảm độc tố trong hạt"
  ],
  answer: 2,
  explain: "Nấm mốc phát triển mạnh trong môi trường giàu chất dinh dưỡng → gây hỏng thực phẩm."
},
{
  id: 64,
  q: "Độc tố aflatoxin nguy hiểm do nấm mốc nào sinh ra?",
  choices: [
    "Saccharomyces cerevisiae",
    "Aspergillus flavus",
    "Penicillium camemberti",
    "Candida albicans"
  ],
  answer: 1,
  explain: "Aspergillus flavus và A. parasiticus tạo aflatoxin – độc tố gây ung thư gan."
},
{
  id: 65,
  q: "Nấm mốc gây bệnh actinomycosis ở người?",
  choices: [
    "Đúng",
    "Sai"
  ],
  answer: 1,
  explain: "Actinomycosis do xạ khuẩn (Actinomyces), không phải nấm mốc."
},

{
  id: 66,
  q: "Đặc điểm nào đúng về hình dạng của tế bào nấm men?",
  choices: [
    "Có hình que dài tương tự vi khuẩn Gram âm",
    "Có hình sao hoặc đa giác bất định",
    "Có hình cầu, bầu dục hoặc elip",
    "Luôn tạo thành sợi nấm hoàn chỉnh"
  ],
  answer: 2,
  explain: "Nấm men là vi sinh vật nhân thực, đơn bào, có hình dạng đặc trưng là cầu, bầu dục hoặc elip với kích thước 3–7 µm. Chúng không có hình que hay hình sao, và cũng không tạo thành sợi nấm hoàn chỉnh như nấm mốc."
},
{
  id: 67,
  q: "Hình thức sinh sản chủ yếu của nấm men là gì?",
  choices: [
    "Nảy chồi",
    "Tạo bào tử nang dày",
    "Phân mảnh sợi nấm",
    "Nội phân bào nhiều nhân"
  ],
  answer: 0,
  explain: "Nấm men sinh sản chủ yếu bằng nảy chồi, trong đó một tế bào con nhỏ mọc từ tế bào mẹ. Một số loài có thể sinh sản bằng phân đôi, nhưng nảy chồi là phổ biến nhất."
},
{
  id: 68,
  q: "Chuỗi tế bào nối tiếp nhau do nấm men tạo thành được gọi là gì?",
  choices: [
    "Hyphae thật sự",
    "Sợi nấm đơn tính",
    "Pseudohyphae (chuỗi giả khuẩn ty)",
    "Chuỗi sợi ti thể"
  ],
  answer: 2,
  explain: "Khi tế bào nấm men nảy chồi nhưng không tách rời hoàn toàn, chúng tạo thành pseudohyphae – chuỗi giả khuẩn ty. Đây không phải là sợi nấm thật như ở nấm mốc."
},
{
  id: 69,
  q: "Vai trò có lợi quan trọng nhất của Saccharomyces cerevisiae là gì?",
  choices: [
    "Phân giải chất béo thành acid béo",
    "Tạo protein để lên men đậu nành",
    "Lên men rượu, tạo ethanol và CO₂",
    "Tổng hợp độc tố diệt khuẩn"
  ],
  answer: 2,
  explain: "Saccharomyces cerevisiae là loài nấm men nổi tiếng dùng trong lên men rượu, chuyển hóa đường thành ethanol và CO₂, được ứng dụng trong sản xuất rượu, bia và bánh mì."
},
{
  id: 70,
  q: "Loài nấm men nào có thể gây bệnh ở người, đặc biệt là nhiễm nấm Candida?",
  choices: [
    "Penicillium notatum",
    "Aspergillus fumigatus",
    "Candida albicans",
    "Rhizopus stolonifer"
  ],
  answer: 2,
  explain: "Candida albicans là loài nấm men gây bệnh phổ biến ở người, gây nhiễm nấm Candida ở miệng, da, niêm mạc và cơ quan sinh dục. Các loài khác là nấm mốc, không phải nấm men gây bệnh đặc trưng này."
},

{
  id: 71,
  q: "Đặc điểm nào sau đây đúng với tảo?",
  choices: [
    "Là vi sinh vật nhân sơ không có diệp lục",
    "Là nấm đơn bào có khả năng phân giải cellulose",
    "Là vi sinh vật nhân thực có diệp lục và khả năng quang hợp",
    "Là vi khuẩn sống ký sinh bắt buộc"
  ],
  answer: 2,
  explain: "Tảo là vi sinh vật nhân thực, có diệp lục và khả năng quang hợp, giúp chúng tự dưỡng. Chúng không phải vi khuẩn hay nấm."
},
{
  id: 72,
  q: "Tảo chủ yếu sống ở môi trường nào?",
  choices: [
    "Môi trường khô hoàn toàn như sa mạc cát",
    "Các khu vực núi lửa có nhiệt độ cực cao",
    "Môi trường nước hoặc nơi ẩm ướt",
    "Trong mô động vật sống như ký sinh trùng"
  ],
  answer: 2,
  explain: "Tảo sống chủ yếu trong nước ngọt, nước mặn hoặc nơi ẩm ướt. Chúng không sống ở môi trường khô kiệt hay nội bào động vật."
},
{
  id: 73,
  q: "Sắc tố nào góp phần tạo màu sắc đa dạng cho tảo?",
  choices: [
    "Hemoglobin",
    "Melanin",
    "Diệp lục, carotenoid và phycocyanin",
    "Riboflavin"
  ],
  answer: 2,
  explain: "Tảo có màu sắc phong phú nhờ nhiều loại sắc tố như diệp lục, carotenoid, phycocyanin. Đây là các sắc tố quang hợp đặc trưng của tảo."
},
{
  id: 74,
  q: "Loại sản phẩm công nghiệp nào được tạo ra từ tảo?",
  choices: [
    "Collagen động vật",
    "Agar, carrageenan, alginat",
    "Penicillin",
    "Casein sữa"
  ],
  answer: 1,
  explain: "Tảo (đặc biệt tảo đỏ và tảo nâu) được dùng để sản xuất agar, carrageenan, alginat, ứng dụng trong thực phẩm và công nghiệp."
},
{
  id: 75,
  q: "Tác hại nào sau đây liên quan đến tảo?",
  choices: [
    "Gây bệnh lao cho người",
    "Phân hủy kim loại nặng trong nước",
    "Làm tăng pH của đất dẫn tới hoang mạc hóa",
    "Gây hiện tượng “nở hoa nước” và sinh độc tố"
  ],
  answer: 3,
  explain: "Một số tảo có thể gây phú dưỡng, nở hoa nước (algal bloom) và sản sinh độc tố gây chết cá hoặc gây ngộ độc (như hiện tượng thủy triều đỏ – red tide)."
},

/*chương 3*/ 
 
{
  id: 76,
  q: "Ở pha Lag, vi khuẩn chủ yếu thực hiện hoạt động nào?",
  choices: [
    "Tăng số lượng theo cấp số nhân",
    "Chết hàng loạt do độc tố tích tụ",
    "Chưa phân chia mà đang thích nghi với môi trường mới",
    "Ngừng mọi hoạt động trao đổi chất"
  ],
  answer: 2,
  explain: "Pha Lag là giai đoạn thích nghi, vi khuẩn chưa phân chia mà tập trung tổng hợp enzyme và chuẩn bị cho sự tăng trưởng."
},
{
  id: 77,
  q: "Đặc điểm quan trọng nhất của pha Log là gì?",
  choices: [
    "Không có sự thay đổi về số lượng tế bào",
    "Tế bào phân chia chậm và không ổn định",
    "Vi khuẩn tăng số lượng theo cấp số nhân",
    "Tế bào ngừng sinh sản và bắt đầu tự phân giải"
  ],
  answer: 2,
  explain: "Pha Log (logarit) là giai đoạn tăng trưởng nhanh nhất, số lượng vi khuẩn tăng theo cấp số nhân."
},
{
  id: 78,
  q: "Điều gì xảy ra trong pha cân bằng (pha ổn định)?",
  choices: [
    "Vi khuẩn đạt tốc độ sinh trưởng cao nhất",
    "Số tế bào sinh ra bằng số tế bào chết",
    "Không có tế bào nào chết trong giai đoạn này",
    "Tế bào giảm kích thước nhưng vẫn tăng nhanh về số lượng"
  ],
  answer: 1,
  explain: "Pha cân bằng là lúc tổng số tế bào không đổi vì tốc độ sinh và chết bằng nhau, do cạn dinh dưỡng và tích tụ chất thải."
},
{
  id: 79,
  q: "Tại sao vi khuẩn bước vào pha suy vong?",
  choices: [
    "Vì tế bào nhân lên quá nhanh làm vỡ môi trường",
    "Vì vi khuẩn ngừng hấp thu nước từ môi trường",
    "Vì thiếu dinh dưỡng, tích tụ độc tố và tế bào tự phân giải",
    "Vì vi khuẩn bị ánh sáng mạnh làm bất hoạt hoàn toàn"
  ],
  answer: 2,
  explain: "Pha suy vong xảy ra khi độc tố tích tụ, dinh dưỡng cạn kiệt, và tế bào tự phân giải, khiến số lượng tế bào sống giảm mạnh."
},
{
  id: 80,
  q: "Nhận định nào mô tả đúng mô hình sinh trưởng trong nuôi cấy tĩnh?",
  choices: [
    "Vi khuẩn liên tục tăng sinh suốt quá trình vì dinh dưỡng luôn được thêm mới",
    "Vi khuẩn được cung cấp môi trường hoàn toàn vô trùng nên không có pha chết",
    "Vi khuẩn trải qua 4 pha: Lag → Log → Cân bằng → Suy vong",
    "Vi khuẩn chỉ có 2 pha sinh trưởng do không trao đổi chất"
  ],
  answer: 2,
  explain: "Trong nuôi cấy tĩnh, vi khuẩn luôn trải qua 4 pha đặc trưng: Lag, Log, Cân bằng và Suy vong — do điều kiện không được bổ sung dinh dưỡng và không loại bỏ chất thải."
},

{
  id: 81,
  q: "Tại sao trong sản xuất người ta thường thu hoạch enzyme hoặc sinh khối vào cuối pha log?",
  choices: [
    "Vì đây là lúc vi khuẩn ngừng hoạt động hoàn toàn",
    "Vì tế bào đang hoạt động mạnh và ổn định nhất",
    "Vì đây là lúc vi khuẩn tự phân giải mạnh",
    "Vì số lượng tế bào giảm xuống mức thấp nhất"
  ],
  answer: 1,
  explain: "Cuối pha log/đầu pha ổn định là thời điểm tế bào hoạt động mạnh, ổn định, thuận lợi nhất để thu sản phẩm sinh học."
},
{
  id: 82,
  q: "Tại sao giống vi khuẩn nên được cấy chuyền ở pha log?",
  choices: [
    "Vì vi khuẩn đang chết hàng loạt",
    "Vì vi khuẩn bất hoạt nên dễ kiểm soát",
    "Vì vi khuẩn tăng trưởng nhanh và ổn định, không bị kéo dài pha Lag",
    "Vì vi khuẩn ít trao đổi chất nên không cạnh tranh dinh dưỡng"
  ],
  answer: 2,
  explain: "Cấy ở pha log giúp giảm hoặc tránh pha Lag, khiến quá trình lên men diễn ra nhanh và ổn định."
},
{
  id: 83,
  q: "Để tăng sinh khối vi khuẩn trong sản xuất, người ta cần làm gì?",
  choices: [
    "Giảm pH xuống mức cực thấp",
    "Tăng chất độc trong môi trường nuôi",
    "Kéo dài pha log bằng cách điều chỉnh môi trường, nhiệt độ, pH",
    "Giảm dinh dưỡng để vi khuẩn không phân chia"
  ],
  answer: 2,
  explain: "Muốn tăng sinh khối phải duy trì pha log càng lâu càng tốt, bằng cách tối ưu môi trường nuôi cấy."
},
{
  id: 84,
  q: "Tại sao hệ thống nuôi cấy liên tục lại dựa vào pha cân bằng của đường cong sinh trưởng?",
  choices: [
    "Vì số lượng tế bào luôn giảm nhanh",
    "Vì vi khuẩn không còn khả năng trao đổi chất",
    "Vì số lượng tế bào ổn định, thích hợp cho sản xuất liên tục",
    "Vì tế bào ở pha này không cần cung cấp dinh dưỡng"
  ],
  answer: 2,
  explain: "Trong pha cân bằng, tốc độ sinh và chết bằng nhau → số lượng tế bào ổn định, thích hợp cho hệ thống sản xuất quy mô lớn, liên tục."
},
{
  id: 85,
  q: "Tại sao hiểu tốc độ phát triển vi khuẩn gây bệnh lại quan trọng trong y học?",
  choices: [
    "Vì giúp quyết định thời điểm cho bệnh nhân nghỉ ngơi",
    "Vì có thể điều trị hiệu quả trước khi vi khuẩn bước vào pha log",
    "Vì vi khuẩn chỉ gây bệnh khi ở pha suy vong",
    "Vì vi khuẩn chỉ tồn tại trong môi trường bên ngoài"
  ],
  answer: 1,
  explain: "Pha log là lúc vi khuẩn phát triển bùng nổ. Phát hiện và điều trị sớm trước pha này giúp hiệu quả hơn."
},
{
  id: 86,
  q: "Ứng dụng của đường cong sinh trưởng trong kiểm soát nhiễm khuẩn là gì?",
  choices: [
    "Khử trùng khi vi khuẩn ngừng trao đổi chất",
    "Khử trùng trước khi vi khuẩn đạt tốc độ tăng nhanh",
    "Chỉ khử trùng khi vi khuẩn bước vào pha suy vong",
    "Khử trùng ngẫu nhiên không theo thời điểm"
  ],
  answer: 1,
  explain: "Đường cong giúp biết thời điểm vi khuẩn sắp vào pha log, từ đó khử trùng trước khi chúng tăng sinh mạnh."
},
{
  id: 87,
  q: "Tại sao pha log là thời điểm thích hợp để lấy kháng nguyên làm vaccine?",
  choices: [
    "Vì vi khuẩn không có độc tố",
    "Vì vi khuẩn đang chết dần nên dễ thu",
    "Vì số lượng vi khuẩn lớn nhất và hoạt động mạnh",
    "Vì tế bào ngừng tạo protein"
  ],
  answer: 2,
  explain: "Cuối pha log, số lượng tế bào nhiều nhất, hoạt động mạnh → thuận lợi để thu kháng nguyên."
},
{
  id: 88,
  q: "Trong bảo quản thực phẩm, mục tiêu chính khi tác động lên điều kiện môi trường là gì?",
  choices: [
    "Làm vi khuẩn bước vào pha log nhanh hơn",
    "Làm vi khuẩn không thể vào pha log",
    "Tăng tốc độ trao đổi chất của vi khuẩn",
    "Kéo dài pha log để tăng sinh sản"
  ],
  answer: 1,
  explain: "Bảo quản nhằm ngăn không cho vi khuẩn bước vào pha log, bằng cách giảm nhiệt độ, giảm nước, tăng đường/muối."
},
{
  id: 89,
  q: "Làm thế nào để xác định thời gian an toàn của thực phẩm?",
  choices: [
    "Dựa vào tốc độ vi khuẩn phân hủy protein",
    "Dựa vào khả năng vi khuẩn tạo bào tử",
    "Dựa vào điều kiện khiến vi khuẩn có thể hoặc không thể bước vào pha log",
    "Dựa vào số lượng enzyme có trong thực phẩm"
  ],
  answer: 2,
  explain: "Thời gian an toàn phụ thuộc vào điều kiện bảo quản có cho phép vi khuẩn tăng sinh mạnh (pha log) hay không."
},
{
  id: 90,
  q: "Trong nghiên cứu vi sinh, đường cong sinh trưởng giúp xác định thông số nào?",
  choices: [
    "Khối lượng phân tử của enzyme",
    "Tốc độ sinh trưởng và thời gian thế hệ",
    "Màu sắc khuẩn lạc",
    "Cấu trúc DNA của vi khuẩn"
  ],
  answer: 1,
  explain: "Đường cong sinh trưởng giúp xác định tốc độ sinh trưởng, thời gian thế hệ, rất cần trong thí nghiệm và phân lập."
},

{
  id: 91,
  q: "Vi sinh vật tự dưỡng cacbon sử dụng nguồn cacbon nào để tổng hợp chất hữu cơ?",
  choices: [
    "Chỉ từ protein động vật",
    "Từ lipid của sinh vật khác",
    "Từ CO₂ hoặc muối cacbonat (nguồn cacbon vô cơ)",
    "Từ đường glucose trong môi trường"
  ],
  answer: 2,
  explain: "Nhóm tự dưỡng cacbon dùng CO₂ hoặc muối cacbonat làm nguồn cacbon để tạo chất hữu cơ của tế bào."
},
{
  id: 92,
  q: "Vi sinh vật tự dưỡng cacbon cần nguồn năng lượng từ đâu?",
  choices: [
    "Từ quá trình quang hợp của cây xanh",
    "Từ phân giải chất hữu cơ",
    "Từ ánh sáng hoặc từ phản ứng oxy hóa vô cơ",
    "Từ sự phân rã phóng xạ của khoáng chất"
  ],
  answer: 2,
  explain: "Vì CO₂ không tự chuyển hóa, chúng cần năng lượng từ ánh sáng (quang tự dưỡng) hoặc oxy hóa chất vô cơ (hóa tự dưỡng)."
},
{
  id: 93,
  q: "Vi sinh vật quang tự dưỡng sử dụng nguồn năng lượng nào?",
  choices: [
    "Ánh sáng mặt trời",
    "Nhiệt độ cao",
    "Sóng âm",
    "Sự phân hủy chất hữu cơ"
  ],
  answer: 0,
  explain: "Quang tự dưỡng dùng ánh sáng mặt trời làm nguồn năng lượng, nhờ có các sắc tố quang hợp."
},
{
  id: 94,
  q: "Sắc tố quang hợp phổ biến ở vi sinh vật quang tự dưỡng là gì?",
  choices: [
    "Melanin",
    "Xanthophyll",
    "Bacteriochlorophyll",
    "Rhodopsin thần kinh"
  ],
  answer: 2,
  explain: "Nhiều vi sinh vật quang tự dưỡng có sắc tố bacteriochlorophyll dùng để hấp thụ ánh sáng."
},
{
  id: 95,
  q: "Ví dụ nào sau đây thuộc nhóm quang tự dưỡng?",
  choices: [
    "Vi khuẩn nitrat hóa",
    "Vi khuẩn oxy hóa sắt",
    "Vi khuẩn lưu huỳnh màu tía",
    "Vi khuẩn amoni hóa"
  ],
  answer: 2,
  explain: "Vi khuẩn lưu huỳnh màu tía sử dụng ánh sáng, thuộc nhóm quang tự dưỡng."
},
{
  id: 96,
  q: "Vi sinh vật hóa tự dưỡng lấy năng lượng từ đâu?",
  choices: [
    "Oxy hóa các chất vô cơ như NH₃, NO₂⁻, H₂S, Fe²⁺",
    "Phân giải đường từ môi trường",
    "Hấp thu trực tiếp ATP từ sinh vật khác",
    "Phân hủy cellulose"
  ],
  answer: 0,
  explain: "Hóa tự dưỡng dùng phản ứng oxy hóa vô cơ để lấy năng lượng rồi khử CO₂ thành chất hữu cơ."
},
{
  id: 97,
  q: "Ví dụ nào sau đây là vi khuẩn hóa tự dưỡng?",
  choices: [
    "Tảo lam",
    "Nitrosomonas hoặc Nitrobacter",
    "Vi khuẩn lactic",
    "Nấm men Saccharomyces"
  ],
  answer: 1,
  explain: "Nitrosomonas và Nitrobacter là vi khuẩn nitrat hóa, dùng năng lượng oxy hóa NH₃ và NO₂⁻ → thuộc nhóm hóa tự dưỡng."
},
{
  id: 98,
  q: "Vai trò của vi sinh vật tự dưỡng hóa năng trong hệ sinh thái là gì?",
  choices: [
    "Tạo pheromone cho côn trùng",
    "Phân giải nhựa tổng hợp",
    "Tham gia các chu trình sinh địa hóa như chu trình nitơ, lưu huỳnh",
    "Làm tăng độ mặn của đất"
  ],
  answer: 2,
  explain: "Hóa tự dưỡng tham gia quan trọng trong chu trình nitơ, lưu huỳnh, sắt, giúp duy trì cân bằng sinh thái."
},
{
  id: 99,
  q: "Đặc điểm chung của vi sinh vật tự dưỡng cacbon là gì?",
  choices: [
    "Cần glucose từ môi trường để tạo chất hữu cơ",
    "Chỉ sống trong điều kiện kỵ khí tuyệt đối",
    "Tự tổng hợp chất hữu cơ từ CO₂",
    "Chỉ tồn tại ở nhiệt độ cực thấp"
  ],
  answer: 2,
  explain: "Tất cả vi sinh vật tự dưỡng cacbon đều tự tạo chất hữu cơ từ CO₂, không phụ thuộc nguồn cacbon hữu cơ."
},
{
  id: 100,
  q: "Vai trò của tảo lam (cyanobacteria) sống cộng sinh là gì?",
  choices: [
    "Làm tăng nồng độ kim loại nặng trong đất",
    "Gây phân hủy chất hữu cơ trong đất",
    "Cải tạo đất, cung cấp dinh dưỡng cho cây trồng",
    "Làm giảm lượng nitơ trong đất"
  ],
  answer: 2,
  explain: "Tảo lam có thể cố định nitơ, góp phần cải tạo đất và hỗ trợ cây trồng, đặc biệt trong hệ sinh thái ruộng lúa."
},

{
  id: 101,
  q: "Vi sinh vật tự dưỡng amin có khả năng gì?",
  choices: [
    "Chỉ hấp thu acid amin từ môi trường ngoài",
    "Tự tổng hợp tất cả acid amin cần thiết từ NH₃ hoặc muối amon",
    "Chỉ tổng hợp được 1–2 acid amin cơ bản",
    "Không thể tổng hợp protein"
  ],
  answer: 1,
  explain: "Nhóm này có đủ enzyme để tự tổng hợp toàn bộ acid amin từ nitơ vô cơ như NH₃/NH₄⁺."
},
{
  id: 102,
  q: "Vi sinh vật tự dưỡng amin sử dụng nguồn nitơ chính nào?",
  choices: [
    "Nitơ hữu cơ phức tạp từ mô động vật",
    "Chỉ NO₃⁻ từ đất",
    "NH₃ hoặc NH₄⁺",
    "N₂ từ khí trời mà không cần enzyme"
  ],
  answer: 2,
  explain: "Chúng dùng NH₃ hoặc NH₄⁺ để tổng hợp acid amin và protein."
},
{
  id: 103,
  q: "Chức năng quan trọng của hệ enzyme ở vi sinh vật tự dưỡng amin là gì?",
  choices: [
    "Chuyển acid béo thành đường",
    "Chuyển nitơ vô cơ thành acid amin",
    "Gây phân giải DNA",
    "Tổng hợp độc tố ngoại bào"
  ],
  answer: 1,
  explain: "Nhóm này có hệ enzyme hoàn chỉnh giúp chuyển nitơ vô cơ → acid amin, tạo nên nguyên sinh chất."
},
{
  id: 104,
  q: "Đặc điểm nào đúng với vi sinh vật tự dưỡng amin?",
  choices: [
    "Không thể tạo protein",
    "Phải lấy acid amin từ môi trường",
    "Tồn tại ở nhiều nhóm vi khuẩn sống tự do",
    "Chỉ sống ký sinh trên động vật"
  ],
  answer: 2,
  explain: "Nhóm tự dưỡng amin thường sống tự do và có khả năng tự tổng hợp acid amin, không cần phụ thuộc môi trường hữu cơ."
},
{
  id: 105,
  q: "Vi sinh vật dị dưỡng amin khác vi sinh vật tự dưỡng amin ở điểm nào?",
  choices: [
    "Dị dưỡng amin có khả năng quang hợp mạnh hơn",
    "Dị dưỡng amin tự tổng hợp được tất cả acid amin",
    "Dị dưỡng amin không tổng hợp được một số acid amin, phải lấy từ môi trường",
    "Dị dưỡng amin không thể sử dụng NH₄⁺"
  ],
  answer: 2,
  explain: "Dị dưỡng amin cần acid amin có sẵn vì không thể tự tổng hợp đầy đủ."
},
{
  id: 106,
  q: "Cách xác định một chủng có phải là vi sinh vật tự dưỡng amin là gì?",
  choices: [
    "Cấy trên môi trường không có nguồn nitơ",
    "Cấy trên môi trường chỉ có muối amon làm nguồn nitơ",
    "Cấy trên môi trường chỉ chứa CO₂",
    "Cấy trên môi trường giàu acid amin"
  ],
  answer: 1,
  explain: "Nếu vi khuẩn phát triển trên môi trường chỉ chứa NH₄⁺, chứng tỏ nó tự dưỡng amin."
},
{
  id: 107,
  q: "Nếu một chủng vi khuẩn không phát triển trên môi trường chỉ chứa muối amon nhưng phát triển khi bổ sung acid amin, đó là loại gì?",
  choices: [
    "Quang tự dưỡng",
    "Kỵ khí tuyệt đối",
    "Vi sinh vật dị dưỡng amin",
    "Vi khuẩn hóa tự dưỡng"
  ],
  answer: 2,
  explain: "Không phát triển với NH₄⁺ → không tự tổng hợp được acid amin → là dị dưỡng amin."
},
{
  id: 108,
  q: "Vai trò nào sau đây thuộc về vi sinh vật tự dưỡng amin?",
  choices: [
    "Phân giải cellulose làm sạch môi trường",
    "Tạo sinh khối trong tự nhiên",
    "Tạo khí methane trong điều kiện yếm khí",
    "Gây bệnh cho thực vật"
  ],
  answer: 1,
  explain: "Vì tự tổng hợp acid amin và protein, chúng tạo sinh khối đầu tiên trong chuỗi dinh dưỡng."
},
{
  id: 109,
  q: "Vi sinh vật tự dưỡng amin có lợi thế gì trong công nghiệp lên men?",
  choices: [
    "Cần môi trường rất giàu acid amin để phát triển",
    "Dễ nuôi vì không cần bổ sung acid amin vào môi trường",
    "Bị ức chế khi có NH₄⁺",
    "Không thể được sử dụng trong sản xuất sinh khối"
  ],
  answer: 1,
  explain: "Do tự tổng hợp acid amin, chúng không cần môi trường giàu acid amin, giúp giảm chi phí nuôi cấy."
},
{
  id: 110,
  q: "Vì sao vi sinh vật tự dưỡng amin quan trọng trong nghiên cứu dinh dưỡng vi sinh vật?",
  choices: [
    "Vì chúng chỉ sống ở môi trường khắc nghiệt",
    "Vì dễ quan sát bằng mắt thường",
    "Vì không cần kiểm soát nguồn nitơ",
    "Vì giúp nghiên cứu quá trình tổng hợp acid amin và nhu cầu dinh dưỡng của tế bào"
  ],
  answer: 3,
  explain: "Nhờ khả năng tự tổng hợp acid amin, chúng là mô hình tốt để nghiên cứu sinh tổng hợp amino acid và nhu cầu nitơ."
},

{
  id: 111,
  q: "Nhiệt độ tối thiểu ảnh hưởng đến vi sinh vật theo cơ chế nào?",
  choices: [
    "Enzyme hoạt động yếu và màng tế bào bị “đóng băng”",
    "Enzyme hoạt động mạnh nhất",
    "Vi khuẩn phân chia với tốc độ tối đa",
    "Tế bào tăng sinh độc tố để thích nghi"
  ],
  answer: 0,
  explain: "Ở nhiệt độ tối thiểu, hoạt động enzyme giảm, màng giảm tính linh động → vi khuẩn ngừng sinh trưởng."
},
{
  id: 112,
  q: "Nhóm vi sinh vật nào có nhiệt độ tối ưu thuộc khoảng 20–45°C?",
  choices: [
    "Ưa trung nhiệt (Mesophiles)",
    "Ưa lạnh",
    "Ưa muối",
    "Ưa áp suất cao"
  ],
  answer: 0,
  explain: "Mesophiles phát triển mạnh ở 20–45°C, đa số vi khuẩn gây bệnh người thuộc nhóm này."
},
{
  id: 113,
  q: "Điều gì xảy ra khi nhiệt độ vượt mức tối đa của vi sinh vật?",
  choices: [
    "Protein và enzyme bị biến tính dẫn đến chết tế bào",
    "Vi sinh vật sinh trưởng mạnh hơn",
    "Vi khuẩn ngủ đông",
    "Tăng tổng hợp DNA"
  ],
  answer: 0,
  explain: "Nhiệt độ cao phá hủy protein và màng tế bào → chết."
},
{
  id: 114,
  q: "Nhóm vi sinh vật nào có khả năng phát triển ở trên 80°C?",
  choices: [
    "Siêu ưa nhiệt",
    "Ưa kiềm",
    "Ưa mặn",
    "Ưa lạnh"
  ],
  answer: 0,
  explain: "Hyperthermophiles sống ở >80°C."
},
{
  id: 115,
  q: "Vì sao bảo quản thực phẩm bằng lạnh lại hạn chế vi khuẩn phát triển?",
  choices: [
    "Làm chậm hoạt động enzyme, ngăn vi khuẩn vào pha log",
    "Làm tăng áp suất trong tế bào",
    "Tăng tốc độ biến tính protein",
    "Cung cấp thêm dinh dưỡng"
  ],
  answer: 0,
  explain: "Lạnh làm vi khuẩn không thể tăng trưởng nhanh → hạn chế hư thực phẩm."
},
{
  id: 116,
  q: "Nhiệt độ tối ưu của các vi khuẩn ưa nhiệt nằm trong khoảng:",
  choices: [
    "55–65°C",
    "0–20°C",
    "80–100°C",
    "15–25°C"
  ],
  answer: 0,
  explain: "Thermophiles phát triển mạnh ở 55–65°C."
},
{
  id: 117,
  q: "Trong nuôi cấy vi sinh vật, vì sao phải duy trì nhiệt độ ổn định?",
  choices: [
    "Vì mỗi loài có nhiệt độ tối ưu riêng",
    "Vì nhiệt độ không ảnh hưởng đến enzyme",
    "Vì chỉ vi khuẩn gây bệnh mới nhạy cảm với nhiệt",
    "Vì enzyme hoạt động tốt ở mọi mức nhiệt"
  ],
  answer: 0,
  explain: "Nhiệt độ quyết định tốc độ sinh trưởng và enzyme."
},
{
  id: 118,
  q: "Đặc điểm của vi khuẩn ưa lạnh là:",
  choices: [
    "Nhiệt độ tối ưu khoảng 15°C",
    "Chỉ sống ở 55–65°C",
    "Chỉ tồn tại trong môi trường khô",
    "Không thể phát triển dưới 30°C"
  ],
  answer: 0,
  explain: "Psychrophiles thích nghi tốt với môi trường lạnh."
},
{
  id: 119,
  q: "Phương pháp tiệt trùng bằng hấp 121°C dựa trên cơ chế nào?",
  choices: [
    "Làm biến tính protein và phá vỡ màng tế bào",
    "Làm vi khuẩn ngủ đông",
    "Ngừng trao đổi chất nhưng không giết vi khuẩn",
    "Tăng tốc độ phân chia làm vi khuẩn tự chết"
  ],
  answer: 0,
  explain: "Nhiệt cao phá hủy protein → tiệt trùng hiệu quả."
},
{
  id: 120,
  q: "Tại sao vi sinh vật không thể phát triển khi xuống dưới nhiệt độ tối thiểu?",
  choices: [
    "Màng tế bào giảm tính linh động, enzyme hoạt động yếu",
    "Tế bào già đi",
    "Áp suất môi trường giảm",
    "Thiếu oxy"
  ],
  answer: 0,
  explain: "Màng gần như đóng băng → trao đổi chất giảm mạnh, sinh trưởng dừng."
},

{
  id: 121,
  q: "Tác động đặc trưng của tia UV lên DNA vi sinh vật là gì?",
  choices: [
    "Tạo liên kết dimer thymine gây đột biến",
    "Làm DNA xoắn chặt hơn giúp vi khuẩn ổn định",
    "Tăng tốc độ sao chép DNA",
    "Tạo màng bảo vệ chống đột biến"
  ],
  answer: 0,
  explain: "UV gây dimer thymine → cản trở sao chép → đột biến hoặc chết tế bào."
},
{
  id: 122,
  q: "Vì sao tia UV chủ yếu chỉ khử trùng được bề mặt?",
  choices: [
    "Khả năng xuyên thấm kém",
    "Tương tác mạnh với nước làm mất tác dụng",
    "Bị enzyme phân hủy nhanh",
    "Chỉ hoạt động khi có oxy cao"
  ],
  answer: 0,
  explain: "UV không xuyên sâu → dùng cho bề mặt, không khí."
},
{
  id: 123,
  q: "Tia gamma gây chết vi sinh vật chủ yếu nhờ cơ chế nào?",
  choices: [
    "Phá hủy DNA và tạo gốc tự do",
    "Làm đông cứng tế bào",
    "Giảm pH tế bào",
    "Tăng áp suất thẩm thấu"
  ],
  answer: 0,
  explain: "Tia ion hóa (gamma, X) phá hủy DNA và tạo gốc tự do rất mạnh."
},
{
  id: 124,
  q: "Ứng dụng phổ biến của tia ion hóa (gamma, X) trong công nghiệp là gì?",
  choices: [
    "Tiệt trùng dụng cụ y tế và thực phẩm",
    "Tăng sinh trưởng của vi khuẩn",
    "Tạo màu thực phẩm",
    "Khử độc kim loại nặng"
  ],
  answer: 0,
  explain: "Gamma dùng để tiệt trùng vì xuyên thấm mạnh."
},
{
  id: 125,
  q: "Tia hồng ngoại tiêu diệt vi sinh vật chủ yếu bằng cách:",
  choices: [
    "Tăng nhiệt làm biến tính protein",
    "Tạo gốc tự do phá DNA",
    "Phá màng sinh học",
    "Ức chế tổng hợp RNA"
  ],
  answer: 0,
  explain: "Hồng ngoại chủ yếu làm nóng → protein biến tính."
},
{
  id: 126,
  q: "Trong các loại vi sinh vật sau, nhóm nào kháng tia bức xạ mạnh nhất?",
  choices: [
    "Vi khuẩn sinh bào tử",
    "Virus không vỏ",
    "Nấm men",
    "Vi khuẩn dạng sinh dưỡng"
  ],
  answer: 0,
  explain: "Bào tử rất bền, chịu nhiệt và bức xạ cao."
},
{
  id: 127,
  q: "Ứng dụng của tia UV trong xử lý nước chủ yếu dựa vào:",
  choices: [
    "Khả năng diệt khuẩn trên bề mặt và trong lớp nước mỏng",
    "Tăng nhiệt giúp nước bay hơi nhanh",
    "Cung cấp năng lượng cho quá trình oxy hóa",
    "Tạo màu cho nước"
  ],
  answer: 0,
  explain: "UV dùng trong xử lý nước vì diệt khuẩn tốt ở lớp nước mỏng."
},
{
  id: 128,
  q: "Tia ion hóa có khả năng xuyên thấm mạnh vì:",
  choices: [
    "Có năng lượng cao",
    "Có bước sóng dài",
    "Thường được kết hợp với nhiệt",
    "Phản ứng với sắc tố tế bào"
  ],
  answer: 0,
  explain: "Gamma/X năng lượng cao → xuyên sâu → dùng để chiếu xạ thực phẩm."
},
{
  id: 129,
  q: "Ứng dụng của bức xạ trong chọn giống vi sinh vật là gì?",
  choices: [
    "Tạo đột biến để chọn chủng năng suất cao",
    "Giảm hoàn toàn đột biến tự nhiên",
    "Giúp vi khuẩn tăng sức đề kháng",
    "Kéo dài pha lag trong nuôi cấy"
  ],
  answer: 0,
  explain: "Bức xạ gây đột biến → chọn lọc chủng tốt hơn."
},
{
  id: 130,
  q: "Virus không vỏ nhạy cảm với bức xạ vì lý do nào?",
  choices: [
    "Không có màng bảo vệ bao quanh vật liệu di truyền",
    "Có protein vỏ quá dày",
    "DNA nằm sâu bên dưới lớp lipid",
    "Có enzyme sửa chữa DNA rất mạnh"
  ],
  answer: 0,
  explain: "Virus không vỏ dễ bị phá hủy DNA bởi tia UV và gamma."
},

/*chương 5*/ 

{
  id: 131,
  q: "Điểm khác biệt lớn nhất giữa virus và vi sinh vật khác là gì?",
  choices: [
    "Không có cấu tạo tế bào",
    "Có kích thước lớn hơn vi khuẩn",
    "Có khả năng tự sinh sản",
    "Có hệ thống enzyme hoàn chỉnh"
  ],
  answer: 0,
  explain: "Virus không có tế bào, chỉ gồm vỏ protein và acid nucleic."
},
{
  id: 132,
  q: "Virus chỉ có thể nhân lên khi:",
  choices: [
    "Ở bên trong tế bào sống của vật chủ",
    "Trong môi trường nhân tạo giàu dinh dưỡng",
    "Có đủ oxy trong không khí",
    "Nhiệt độ dưới 0°C"
  ],
  answer: 0,
  explain: "Virus là ký sinh nội bào bắt buộc, không sinh sản bên ngoài tế bào chủ."
},
{
  id: 133,
  q: "Thành phần hóa học của virus gồm:",
  choices: [
    "Protein và một loại acid nucleic (ADN hoặc ARN)",
    "Protein, lipid, glucid và ADN",
    "ADN và ARN đồng thời",
    "Nhiều loại enzyme hô hấp"
  ],
  answer: 0,
  explain: "Virus chỉ chứa protein và một loại acid nucleic."
},
{
  id: 134,
  q: "Virus không thể tự sinh năng lượng vì:",
  choices: [
    "Không có hệ thống enzyme hô hấp và vận chuyển",
    "Không tiếp xúc được với ánh sáng",
    "Không có màng tế bào",
    "Không có nhân"
  ],
  answer: 0,
  explain: "Virus hoàn toàn phụ thuộc vào tế bào chủ vì thiếu hệ enzyme cần thiết."
},
{
  id: 135,
  q: "Đặc điểm nào sau đây đúng với một số virus?",
  choices: [
    "Có thể tạo tinh thể khi ở ngoài tế bào",
    "Có khả năng tự tổng hợp protein",
    "Có ribosome riêng",
    "Có cả ADN và ARN"
  ],
  answer: 0,
  explain: "Một số virus có khả năng kết tinh khi ở ngoài tế bào — điểm đặc trưng của chúng."
},

{
  id: 136,
  q: "Thành phần nào của virus có chức năng bảo vệ nhân và giữ hình dạng – kích thước của virus?",
  choices: [
    "Envelope",
    "Capsid",
    "Thể bao hàm",
    "Peptidoglycan"
  ],
  answer: 1,
  explain: "Capsid là lớp vỏ protein bao bọc axit nucleic, giúp bảo vệ nhân và duy trì hình dạng virus."
},
{
  id: 137,
  q: "Protome trong cấu trúc virus là gì?",
  choices: [
    "Đơn vị hình thái của capsid",
    "Đơn vị cấu tạo nhỏ nhất của vỏ protein",
    "Một dạng axit nucleic của virus",
    "Bộ phận giúp virus bám tế bào"
  ],
  answer: 1,
  explain: "Protome là đơn vị cấu trúc nhỏ tạo nên capsid và có bản chất là protein."
},
{
  id: 138,
  q: "Virus có thể có kiểu sắp xếp capsid nào sau đây?",
  choices: [
    "Hình que dẹt",
    "Đối xứng hình khối",
    "Lưỡng tính",
    "Hình đa giác 8 mặt"
  ],
  answer: 1,
  explain: "Một trong ba kiểu sắp xếp capsid là đối xứng hình khối (đa diện 20 mặt)."
},
{
  id: 139,
  q: "Nhân virus chứa loại vật chất di truyền nào?",
  choices: [
    "Cả ADN và ARN",
    "ARN sợi kép và ADN sợi đơn",
    "Chỉ chứa một loại axit nucleic",
    "Chỉ protein"
  ],
  answer: 2,
  explain: "Virus chỉ chứa một loại axit nucleic: ADN hoặc ARN."
},
{
  id: 140,
  q: "ADN của virus thường tồn tại dưới dạng gì?",
  choices: [
    "Chuỗi vòng đơn",
    "Sợi kép",
    "Sợi đơn phân mảnh",
    "Sợi xoắn lỏng lẻo"
  ],
  answer: 1,
  explain: "ADN virus thường ở dạng sợi kép."
},
{
  id: 141,
  q: "Vỏ bọc ngoài (envelope) của virus có bản chất là gì?",
  choices: [
    "Peptidoglycan",
    "Lipo–polysaccharide",
    "Lipoprotein – glucoprotein",
    "Protein tinh khiết"
  ],
  answer: 2,
  explain: "Envelope là màng lipoprotein–glucoprotein giúp virus bám và thoát khỏi tế bào."
},
{
  id: 142,
  q: "Chức năng nào sau đây KHÔNG thuộc về envelope của virus?",
  choices: [
    "Giúp virus bám tế bào",
    "Tạo kháng nguyên bề mặt",
    "Tham gia tổng hợp axit nucleic",
    "Giúp virus giải phóng khỏi tế bào"
  ],
  answer: 2,
  explain: "Envelope không tham gia tổng hợp axit nucleic; đó là chức năng của nhân virus."
},
{
  id: 143,
  q: "Thể Negri là dạng thể bao hàm xuất hiện trong bệnh nào?",
  choices: [
    "Bệnh cúm",
    "Bệnh sởi",
    "Bệnh dại",
    "Bệnh quai bị"
  ],
  answer: 2,
  explain: "Thể Negri là thể bao hàm đặc trưng trong tế bào nhiễm virus dại."
},
{
  id: 144,
  q: "Capsome là gì?",
  choices: [
    "Thành phần của envelope",
    "Đơn vị hình thái của capsid",
    "Một loại protein giúp virus nhân lên",
    "Vật chất di truyền của virus"
  ],
  answer: 1,
  explain: "Capsome là đơn vị hình thái cấu tạo nên capsid."
},
{
  id: 145,
  q: "Virus cúm thuộc kiểu sắp xếp capsid nào?",
  choices: [
    "Đối xứng hình trụ",
    "Phức tạp",
    "Xoắn",
    "Lập phương"
  ],
  answer: 2,
  explain: "Virus cúm là ví dụ điển hình của capsid dạng xoắn."
},

{
  id: 146,
  q: "Mục đích nào sau đây không thuộc phương pháp nuôi cấy virus trên động vật cảm thụ?",
  choices: [
    "Phân lập virus",
    "Nghiên cứu bệnh lý",
    "Tăng sinh vi khuẩn",
    "Sản xuất vacxin"
  ],
  answer: 2,
  explain: "Nuôi cấy virus không nhằm tăng sinh vi khuẩn mà nhằm phân lập, nghiên cứu virus và sản xuất vacxin."
},
{
  id: 147,
  q: "Bước nào sau đây nằm trong quá trình chuẩn bị hỗn dịch virus?",
  choices: [
    "Tiêm virus vào mô não",
    "Nghiền bệnh phẩm với dung dịch sinh lý hoặc PBS",
    "Cho động vật nghỉ ngơi 24 giờ",
    "Cho virus vào môi trường thạch"
  ],
  answer: 1,
  explain: "Hỗn dịch virus được chuẩn bị bằng cách nghiền bệnh phẩm với dung dịch sinh lý/PBS."
},
{
  id: 148,
  q: "Khi chuẩn bị hỗn dịch virus, việc thêm kháng sinh nhằm mục đích gì?",
  choices: [
    "Ổn định cấu trúc virus",
    "Loại tạp khuẩn",
    "Tăng độc lực virus",
    "Kích thích miễn dịch"
  ],
  answer: 1,
  explain: "Kháng sinh được thêm vào để loại bỏ vi khuẩn lẫn trong bệnh phẩm."
},
{
  id: 149,
  q: "Loài động vật cảm thụ phù hợp để nuôi cấy virus Newcastle là:",
  choices: [
    "Vịt 1–7 ngày tuổi",
    "Gà giò",
    "Lợn choai",
    "Gà 3–6 tuần tuổi"
  ],
  answer: 1,
  explain: "Virus Newcastle cảm thụ tốt trên gà giò."
},
{
  id: 150,
  q: "Virus Gumboro thường được nuôi cấy trên đối tượng nào?",
  choices: [
    "Gà 3–6 tuần tuổi",
    "Gà giò",
    "Lợn choai",
    "Vịt 1–7 ngày tuổi"
  ],
  answer: 0,
  explain: "Virus Gumboro gây bệnh trên gà 3–6 tuần tuổi nên sử dụng nhóm này để gây nhiễm."
},
{
  id: 151,
  q: "Đường tiêm thích hợp cho các virus hướng thần kinh là:",
  choices: [
    "Tiêm xoang bụng",
    "Khía da",
    "Tiêm vỏ não",
    "Nhỏ mũi"
  ],
  answer: 2,
  explain: "Virus hướng thần kinh được tiêm trực tiếp vào vỏ não để gây nhiễm."
},
{
  id: 152,
  q: "Virus hướng nội bì thường được gây nhiễm bằng cách nào?",
  choices: [
    "Tiêm xoang bụng",
    "Khía hoặc sát da",
    "Tiêm tĩnh mạch",
    "Tiêm cơ"
  ],
  answer: 1,
  explain: "Virus hướng nội bì được gây nhiễm bằng cách khía/sát da."
},
{
  id: 153,
  q: "Virus hướng tạng được gây nhiễm theo đường nào?",
  choices: [
    "Tiêm xoang bụng",
    "Nhỏ mũi",
    "Tiêm vỏ não",
    "Khía da"
  ],
  answer: 0,
  explain: "Virus hướng tạng được tiêm vào xoang bụng để gây nhiễm."
},
{
  id: 154,
  q: "Khi gây nhiễm virus cho động vật cảm thụ, yêu cầu quan trọng là:",
  choices: [
    "Động vật đã từng tiếp xúc với virus",
    "Động vật phải khỏe và chưa nhiễm virus trước đó",
    "Động vật càng già càng tốt",
    "Không cần chọn đúng loài"
  ],
  answer: 1,
  explain: "Động vật phải khỏe và chưa từng tiếp xúc với virus để tránh miễn dịch nền."
},
{
  id: 155,
  q: "Nếu triệu chứng và bệnh tích không rõ ràng sau khi gây nhiễm, bước tiếp theo là gì?",
  choices: [
    "Cho ăn kháng sinh",
    "Gây nhiễm lại ngay lập tức",
    "Dùng phản ứng huyết thanh học để phát hiện kháng thể",
    "Hủy bỏ mẫu thử"
  ],
  answer: 2,
  explain: "Phản ứng huyết thanh học giúp phát hiện các kháng thể đặc hiệu khi bệnh tích không rõ."
},

{
  id: 156,
  q: "Ưu điểm nào sau đây thuộc phương pháp nuôi cấy virus trên phôi gà đang phát triển?",
  choices: [
    "Thực hiện rất khó và tốn kém",
    "Cho kết quả chậm",
    "Thu được lượng virus lớn",
    "Không phù hợp để sản xuất vacxin"
  ],
  answer: 2,
  explain: "Nuôi cấy trên phôi cho phép thu lượng virus nhiều và sử dụng rộng rãi trong sản xuất vacxin."
},
{
  id: 157,
  q: "Khi chuẩn bị hỗn dịch virus để tiêm vào phôi, bước nào sau đây là đúng?",
  choices: [
    "Trộn virus với môi trường thạch",
    "Nghiền và lọc bệnh phẩm, thêm kháng sinh",
    "Hòa virus vào nước cất",
    "Đun nóng bệnh phẩm để vô trùng"
  ],
  answer: 1,
  explain: "Quy trình gồm nghiền – lọc – thêm kháng sinh để loại tạp khuẩn."
},
{
  id: 158,
  q: "Trứng dùng để nuôi cấy virus phải đảm bảo điều kiện nào?",
  choices: [
    "Trứng vỡ nhẹ để dễ thao tác",
    "Trứng càng già càng tốt",
    "Trứng đạt tiêu chuẩn và được ấp đến đúng tuổi phôi",
    "Trứng không cần soi trước khi tiêm"
  ],
  answer: 2,
  explain: "Trứng phải đạt chuẩn và được soi để xác định buồng hơi và vị trí phôi."
},
{
  id: 159,
  q: "Virus dại thường được tiêm vào vị trí nào của phôi gà?",
  choices: [
    "Xoang niệu",
    "Màng niệu–đệm",
    "Khoang màng phổi",
    "Túi lòng đỏ"
  ],
  answer: 3,
  explain: "Virus dại thích hợp nhân lên trong túi lòng đỏ."
},
{
  id: 160,
  q: "Virus Newcastle được tiêm vào vị trí nào của phôi?",
  choices: [
    "Màng niệu–đệm",
    "Xoang niệu",
    "Túi khí",
    "Buồng hơi"
  ],
  answer: 1,
  explain: "Virus Newcastle được gây nhiễm bằng đường tiêm vào xoang niệu."
},
{
  id: 161,
  q: "Virus đậu gà được tiêm vào vị trí nào trong phôi?",
  choices: [
    "Xoang bụng",
    "Màng niệu–đệm",
    "Túi lòng đỏ",
    "Buồng hơi"
  ],
  answer: 1,
  explain: "Virus đậu gà phát triển tốt trong màng niệu–đệm."
},
{
  id: 162,
  q: "Liều thực tế thường tiêm vào mỗi phôi là khoảng:",
  choices: [
    "1 ml/phôi",
    "0,5 ml/phôi",
    "0,2 ml/phôi",
    "0,05 ml/phôi"
  ],
  answer: 2,
  explain: "Liều thực tế thường khoảng 0,2 ml/phôi."
},
{
  id: 163,
  q: "Bước sát trùng buồng hơi trước khi tiêm virus được thực hiện bằng:",
  choices: [
    "Cồn 90°",
    "Cồn iod 5%",
    "Dung dịch clo 2%",
    "Xà phòng sát khuẩn"
  ],
  answer: 1,
  explain: "Buồng hơi được sát trùng bằng cồn iod 5%."
},
{
  id: 164,
  q: "Nhiệt độ ấp trứng sau khi tiêm virus là:",
  choices: [
    "25°C",
    "30°C",
    "37°C",
    "42°C"
  ],
  answer: 2,
  explain: "Trứng sau khi tiêm được ấp ở 37°C."
},
{
  id: 165,
  q: "Sau khi phôi chết, cần bảo quản ở 4°C để làm gì?",
  choices: [
    "Làm chậm sự nhân lên của virus",
    "Giúp mạch máu co lại, dễ quan sát bệnh tích",
    "Làm mềm vỏ trứng để mở dễ hơn",
    "Tiêu diệt toàn bộ virus"
  ],
  answer: 1,
  explain: "Bảo quản 4°C giúp mạch máu co lại, thuận lợi cho việc quan sát bệnh tích."
},

{
  id: 166,
  q: "Nguyên tắc chính của phương pháp nuôi cấy virus trên môi trường tế bào là gì?",
  choices: [
    "Nuôi virus trực tiếp trong máu động vật",
    "Cho virus phát triển trên mô chết",
    "Sử dụng các tế bào sống nuôi trong môi trường nhân tạo để virus nhân lên",
    "Dùng mô đông lạnh để tăng tốc độ nhân lên"
  ],
  answer: 2,
  explain: "Môi trường tế bào cung cấp các tế bào sống để virus xâm nhập và nhân lên."
},
{
  id: 167,
  q: "Môi trường dinh dưỡng nuôi tế bào thường chứa thành phần nào?",
  choices: [
    "Kháng sinh liều cao",
    "Peptidoglycan",
    "Huyết thanh và các chất dinh dưỡng (axit amin, đường, muối khoáng)",
    "Chỉ nước cất vô trùng"
  ],
  answer: 2,
  explain: "Tế bào cần môi trường giàu dinh dưỡng gồm huyết thanh, đường, axit amin và muối."
},
{
  id: 168,
  q: "Tế bào nào sau đây thường được dùng trong nuôi cấy virus?",
  choices: [
    "Hồng cầu người",
    "Tế bào xơ phôi gà",
    "Tế bào sừng hoá",
    "Tế bào gan chết"
  ],
  answer: 1,
  explain: "Tế bào xơ phôi gà là dòng tế bào phổ biến để gây nhiễm nhiều loại virus."
},
{
  id: 169,
  q: "Loại tế bào phù hợp để nuôi cấy virus lở mồm long móng là:",
  choices: [
    "Tế bào biểu bì",
    "BHK hoặc tế bào thận bê",
    "Hồng cầu gà",
    "Tế bào sừng hoá"
  ],
  answer: 1,
  explain: "Virus lở mồm long móng nhân lên tốt trên tế bào BHK và thận bê."
},
{
  id: 170,
  q: "Virus dại có thể được nuôi cấy trên dòng tế bào nào?",
  choices: [
    "Tế bào BHK21, tế bào xơ phôi gà, tế bào thận chuột",
    "Hồng cầu người",
    "Tế bào biểu mô da",
    "Tế bào cơ tim"
  ],
  answer: 0,
  explain: "Virus dại có thể nhân lên trên các dòng tế bào BHK21, xơ phôi gà và thận chuột."
},
{
  id: 171,
  q: "Hiện tượng nào sau đây là một dạng bệnh tích tế bào (CPE)?",
  choices: [
    "Tế bào tăng sinh mạnh",
    "Tế bào xuất hiện hợp bào (syncytium)",
    "Tế bào trở nên trong suốt và khoẻ hơn",
    "Tế bào tăng khả năng phân chia"
  ],
  answer: 1,
  explain: "Hợp bào là hiện tượng nhiều nhân trong một tế bào lớn — đặc trưng của CPE."
},
{
  id: 172,
  q: "Trong CPE, “dung bào” là hiện tượng gì?",
  choices: [
    "Tế bào bị tan rã",
    "Tế bào phân chia quá mức",
    "Tế bào kéo dài thành dạng sợi",
    "Tế bào tích tụ lipid"
  ],
  answer: 0,
  explain: "Dung bào là tế bào bị phá hủy và tan rã khi virus nhân lên mạnh."
},
{
  id: 173,
  q: "Hình thành thể bao hàm trong tế bào nhiễm virus thể hiện điều gì?",
  choices: [
    "Virus bị tế bào tiêu diệt",
    "Virus không thể nhân lên",
    "Virus đang nhân lên và gây biến đổi tế bào",
    "Tế bào trở lại trạng thái bình thường"
  ],
  answer: 2,
  explain: "Thể bao hàm là dấu hiệu virus đang nhân lên trong tế bào."
},
{
  id: 174,
  q: "Quan sát CPE dưới kính hiển vi nhằm mục đích gì?",
  choices: [
    "Xác định virus có nhân lên trong tế bào hay không",
    "Kiểm tra độ tinh khiết của môi trường",
    "Theo dõi hoạt động của vi khuẩn",
    "Đếm số lượng tế bào đang phân chia"
  ],
  answer: 0,
  explain: "Quan sát CPE giúp xác định virus đã gây nhiễm và nhân lên."
},
{
  id: 175,
  q: "Một trong các ý nghĩa quan trọng của phương pháp nuôi cấy virus trên tế bào là:",
  choices: [
    "Chỉ dùng để quan sát hình thái tế bào",
    "Chỉ dùng trong dạy học, không ứng dụng thực tế",
    "Dùng để phân lập, nghiên cứu virus và sản xuất vacxin quy mô lớn",
    "Chỉ dùng để nuôi cấy vi khuẩn"
  ],
  answer: 2,
  explain: "Nuôi cấy tế bào là kỹ thuật hiện đại phục vụ phân lập, nghiên cứu và sản xuất vacxin."
},

{
  id: 176,
  q: "Interferon thuộc loại yếu tố miễn dịch nào?",
  choices: [
    "Miễn dịch đặc hiệu.",
    "Miễn dịch tế bào thuần túy.",
    "Miễn dịch không đặc hiệu.",
    "Miễn dịch dịch thể."
  ],
  answer: 2,
  explain: "Interferon là protein do tế bào sinh ra khi bị virus kích thích và thuộc hệ thống miễn dịch không đặc hiệu."
},
{
  id: 177,
  q: "Interferon được tạo ra khi tế bào bị kích thích bởi yếu tố nào?",
  choices: [
    "Ánh sáng mặt trời.",
    "Virus hoặc tác nhân lạ như vi khuẩn, độc tố.",
    "Hormone tăng trưởng.",
    "Thiếu oxy mô."
  ],
  answer: 1,
  explain: "Tế bào động vật tiết interferon khi bị virus hoặc tác nhân ngoại lai kích thích."
},
{
  id: 178,
  q: "Đặc điểm về tính đặc hiệu của Interferon là gì?",
  choices: [
    "Chỉ đặc hiệu với một loại virus nhất định.",
    "Không đặc hiệu với tế bào sinh ra nó.",
    "Đặc hiệu với tế bào sinh ra nó nhưng không đặc hiệu với loại virus gây kích thích.",
    "Đặc hiệu với tất cả virus cùng một mức độ."
  ],
  answer: 2,
  explain: "Interferon chỉ tác động hiệu quả lên tế bào tạo ra nó, nhưng không phân biệt loại virus kích thích."
},
{
  id: 179,
  q: "Interferon tác động lên tế bào nào đầu tiên?",
  choices: [
    "Chỉ tế bào đã bị nhiễm virus.",
    "Tế bào miễn dịch đặc hiệu.",
    "Tế bào kế bên chưa bị nhiễm virus.",
    "Tế bào thần kinh."
  ],
  answer: 2,
  explain: "Interferon được tiết ra và lan sang tế bào lân cận để kích hoạt cơ chế kháng virus."
},
{
  id: 180,
  q: "Interferon kích hoạt tế bào kế bên tạo ra loại protein nào?",
  choices: [
    "Protein vận chuyển màng.",
    "Enzym tiêu hủy virus trực tiếp.",
    "AVP – antiviral protein.",
    "Protein tổng hợp kháng thể."
  ],
  answer: 2,
  explain: "AVP là protein kháng virus được tạo ra nhờ Interferon."
},
{
  id: 181,
  q: "AVP (antiviral protein) có tác dụng chính gì?",
  choices: [
    "Phá hủy màng protein của virus.",
    "Ngăn sự nhân đôi DNA của tế bào chủ.",
    "Ức chế sao chép thông tin di truyền của virus.",
    "Kích thích virus tạo ARN thông tin."
  ],
  answer: 2,
  explain: "AVP ngăn tạo ARN thông tin của virus → virus không thể tổng hợp protein → ngừng nhân lên."
},
{
  id: 182,
  q: "Interferon ngăn chặn quá trình nào của virus?",
  choices: [
    "Xâm nhập vào tế bào.",
    "Thoát khỏi tế bào.",
    "Sao chép ARN thông tin.",
    "Bám lên bề mặt tế bào."
  ],
  answer: 2,
  explain: "Interferon không ngăn bám hay xâm nhập, mà ức chế giai đoạn sao chép trong tế bào."
},
{
  id: 183,
  q: "Vì sao virus không thể tổng hợp protein khi có Interferon?",
  choices: [
    "Vì virus bị ly giải ngay khi xâm nhập.",
    "Vì tế bào chủ không còn ribosome hoạt động.",
    "Vì không có ARN thông tin để tổng hợp protein.",
    "Vì màng tế bào chủ bị phá hủy."
  ],
  answer: 2,
  explain: "Không có ARN thông tin (ARNtt) → virus không tổng hợp được protein cần thiết."
},
{
  id: 184,
  q: "Nhận định nào sau đây là đúng về khả năng Interferon chống virus?",
  choices: [
    "Tiêu diệt tất cả virus trong cơ thể.",
    "Hoàn toàn đặc hiệu cho từng loại virus.",
    "Có thể ngăn cản sự nhân lên của nhiều loại virus khác nhau.",
    "Chỉ hoạt động khi virus đã nhân lên mạnh."
  ],
  answer: 2,
  explain: "Interferon không đặc hiệu với virus → có thể chống nhiều loại virus khác nhau."
},
{
  id: 185,
  q: "Trong chu trình tác động, bước xảy ra đầu tiên là gì?",
  choices: [
    "Interferon kích hoạt AVP trong tế bào lành.",
    "Virus tổng hợp ARN thông tin.",
    "Tế bào nhiễm virus tạo ra Interferon và tiết ra ngoài.",
    "AVP phân giải màng tế bào chủ."
  ],
  answer: 2,
  explain: "Khi bị nhiễm virus, tế bào đầu tiên sẽ sản xuất Interferon rồi giải phóng ra ngoài."
},

/*chương 6*/ 

{
  id: 186,
  q: "Mục đích chính của phương pháp tiêu độc cơ giới là gì?",
  choices: [
    "Tiêu diệt toàn bộ vi sinh vật bằng nhiệt độ cao.",
    "Làm mất độc tố do vi sinh vật tiết ra.",
    "Giảm số lượng vi sinh vật và làm tăng hiệu quả biện pháp tiêu độc khác.",
    "Tạo môi trường kỵ khí để vi sinh vật không phát triển."
  ],
  answer: 2,
  explain: "Phương pháp cơ giới gồm quét, rửa, cạo… giúp giảm vi sinh vật và hỗ trợ hiệu quả cho tiêu độc hóa học/vật lý."
},
{
  id: 187,
  q: "Cồn etylic 70° được dùng chủ yếu để làm gì?",
  choices: [
    "Tiêu độc chuồng trại.",
    "Khử trùng nước uống.",
    "Sát trùng da.",
    "Khử trùng dụng cụ phẫu thuật bằng nhiệt."
  ],
  answer: 2,
  explain: "Cồn 70° là nồng độ tối ưu để sát trùng da."
},
{
  id: 188,
  q: "Chất nào sau đây thường dùng để khử trùng nước?",
  choices: [
    "Axit phenic 5%.",
    "Cồn iod 1–5%.",
    "Clo và các hợp chất chứa clo.",
    "Cồn etylic 70°."
  ],
  answer: 2,
  explain: "Clo và hợp chất chứa clo có tác dụng mạnh trong khử trùng nước."
},
{
  id: 189,
  q: "Clorua vôi 10% được sử dụng để tiêu độc ở đâu?",
  choices: [
    "Dùng cho da và niêm mạc.",
    "Khử trùng dung dịch nhạy nhiệt.",
    "Khử trùng nước sinh hoạt.",
    "Chuồng trại, đất, phân, phương tiện."
  ],
  answer: 3,
  explain: "Clorua vôi 10% dùng cho môi trường rộng như chuồng trại và chất thải."
},
{
  id: 190,
  q: "Axit phenic 5% (đun sôi) thường được dùng để khử trùng:",
  choices: [
    "Dụng cụ y tế, thú y.",
    "Da động vật.",
    "Không khí trong phòng mổ.",
    "Nước uống."
  ],
  answer: 0,
  explain: "Axit phenic 5% đun sôi có khả năng khử trùng dụng cụ rất mạnh."
},
{
  id: 191,
  q: "Hình thức tiêu độc nào sau đây thuộc phương pháp vật lý?",
  choices: [
    "Dùng clo.",
    "Dùng cồn iod 5%.",
    "Sấy khô ở 180°C/30 phút.",
    "Dùng chế phẩm vi sinh."
  ],
  answer: 2,
  explain: "Sấy ở 180°C/30 phút là ví dụ của nhiệt khô – phương pháp vật lý."
},
{
  id: 192,
  q: "Phương pháp hấp hơi nước ở 120°C/30 phút (Autoclave) có ưu điểm gì?",
  choices: [
    "Chỉ diệt được vi khuẩn dạng hoạt động, không diệt được nha bào.",
    "Dùng được cho các dung dịch nhạy nhiệt.",
    "Diệt được cả nha bào ở điều kiện chuẩn.",
    "Không cần áp suất khi hoạt hóa."
  ],
  answer: 2,
  explain: "Autoclave là phương pháp hiệu quả cao nhất, diệt được cả nha bào."
},
{
  id: 193,
  q: "Phương pháp lọc được sử dụng chủ yếu cho loại vật liệu nào?",
  choices: [
    "Dụng cụ kim loại.",
    "Không khí trong phòng kín.",
    "Dung dịch nhạy nhiệt như huyết thanh, enzyme.",
    "Chuồng trại và đất."
  ],
  answer: 2,
  explain: "Lọc cho phép loại bỏ vi sinh vật mà không cần nhiệt, thích hợp cho dung dịch nhạy nhiệt."
},
{
  id: 194,
  q: "Phương pháp sinh vật học tiêu độc có đặc điểm nào sau đây?",
  choices: [
    "Sử dụng hóa chất mạnh để tiêu diệt vi sinh vật gây bệnh.",
    "Dùng vi sinh vật để ức chế hoặc tiêu diệt vi sinh vật gây bệnh.",
    "Dùng nhiệt độ cao để làm biến tính protein của vi sinh vật.",
    "Dùng tia UV để phá hủy DNA vi khuẩn."
  ],
  answer: 1,
  explain: "Ví dụ điển hình là quá trình ủ phân, sử dụng vi sinh vật có lợi để tiêu hủy mầm bệnh."
},
{
  id: 195,
  q: "Tia UV và tia X được xếp vào nhóm phương pháp tiêu độc nào?",
  choices: [
    "Hóa học.",
    "Cơ giới.",
    "Vật lý.",
    "Sinh học."
  ],
  answer: 2,
  explain: "Chúng là các dạng bức xạ dùng để tiêu diệt vi sinh vật → thuộc phương pháp vật lý."
},

/*thực hành*/ 

{
  id: 196,
  q: "Phương pháp làm tiêu bản cố định có đặc điểm nào sau đây?",
  choices: [
    "Quan sát vi sinh vật sống và khả năng di động của chúng.",
    "Không sử dụng thuốc nhuộm và có thể bảo quản lâu.",
    "Dùng cho vi sinh vật chết, có nhuộm màu trước khi quan sát.",
    "Chỉ dùng để quan sát virus."
  ],
  answer: 2,
  explain: "Tiêu bản cố định dùng để quan sát vi sinh vật đã chết sau khi nhuộm (đơn, Gram, Giemsa…), sau đó rửa – để khô – soi dưới kính hiển vi dầu."
},
{
  id: 197,
  q: "Đặc điểm quan trọng nhất của phương pháp nhuộm đơn là gì?",
  choices: [
    "Vi khuẩn luôn hiện màu tím bất kể thuốc nhuộm.",
    "Chỉ dùng một loại thuốc nhuộm nên vi khuẩn bắt đúng màu của nó.",
    "Cần tẩy màu bằng cồn trước khi nhuộm.",
    "Chỉ áp dụng cho vi khuẩn Gram âm."
  ],
  answer: 1,
  explain: "Nhuộm đơn sử dụng một thuốc nhuộm (fuchsin → đỏ; xanh methylen → xanh; tím gentian → tím), giúp thấy rõ hình dạng và kích thước tế bào."
},
{
  id: 198,
  q: "Nguyên lý giúp vi khuẩn Gram dương giữ được màu tím sau nhuộm Gram là gì?",
  choices: [
    "Thành tế bào mỏng, dễ hút fuchsin sau tẩy màu.",
    "Không có lớp peptidoglycan nên khó tẩy màu.",
    "Thành tế bào dày, nhiều peptidoglycan giữ phức hợp tím gentian – lugol.",
    "Có màng LPS dày ngăn cản cồn xâm nhập."
  ],
  answer: 2,
  explain: "Peptidoglycan dày là lý do chính giúp G+ giữ màu tím; G– bị tẩy màu bởi cồn rồi bắt màu đỏ của fuchsin."
},
{
  id: 199,
  q: "Trong quy trình nhuộm Gram, bước nào quyết định vi khuẩn sẽ là Gram dương hay Gram âm?",
  choices: [
    "Nhỏ tím gentian.",
    "Nhỏ lugol.",
    "Rửa nước sau nhuộm.",
    "Tẩy màu bằng cồn hoặc acetone."
  ],
  answer: 3,
  explain: "Tẩy màu là bước quan trọng nhất: G+ giữ màu tím, G– bị mất màu → nhuộm fuchsin → đỏ/hồng (như E. coli)."
},
{
  id: 200,
  q: "Tiêu bản giọt ép (soi tươi) phù hợp nhất để quan sát hiện tượng nào sau đây?",
  choices: [
    "Hình dạng vi sinh vật sau khi nhuộm màu.",
    "Màu đặc trưng của Gram dương.",
    "Sự di động và nảy chồi của vi sinh vật sống.",
    "Cấu trúc tế bào sau khi đun nóng cố định."
  ],
  answer: 2,
  explain: "Giọt ép không cố định và không nhuộm màu → dùng để quan sát vi sinh vật sống, sự di động, nảy chồi của nấm men… nhưng không lưu giữ lâu."
},




    ];

    // ---------- state ----------
    let originalQuestions = []; // canonical questions (no shuffling of choices)
    let workingQuestions = [];  // questions that may have choices shuffled (saved in snapshot)
    let order = [];
    let state = { currentIndex:0, score:0, answered:{} };

    // ---------- utilities ----------
    function shuffle(array){ for(let i=array.length-1;i>0;i--){ const j=Math.floor(Math.random()*(i+1)); [array[i],array[j]]=[array[j],array[i]] } return array }

    function deepCopy(obj){ return JSON.parse(JSON.stringify(obj)); }

    function shuffleChoicesForQuestion(q){
      // validate question structure
      if(!Array.isArray(q.choices) || q.choices.length < 2 || typeof q.answer !== 'number'){
        console.warn('Question validation failed for id=', q.id);
        return q; // return unmodified
      }
      const idxs = q.choices.map((_, i) => i);
      shuffle(idxs);
      const newChoices = idxs.map(i => q.choices[i]);
      const newAnswer = idxs.indexOf(q.answer);
      return { ...q, choices: newChoices, answer: newAnswer };
    }

    // ---------- persistence ----------
    function saveState(){
      try{
        const toSave = { state, order, timestamp: Date.now() };
        localStorage.setItem(STORAGE_KEY, JSON.stringify(toSave));
        // also save workingQuestions snapshot so that shuffled choices persist across reloads
        localStorage.setItem(SNAPSHOT_KEY, JSON.stringify(workingQuestions));
      }catch(e){ console.warn('saveState error', e); }
      updateLocalInfo();
    }

    function loadState(){
      try{
        const raw = localStorage.getItem(STORAGE_KEY);
        if(!raw) return false;
        const parsed = JSON.parse(raw);
        if(parsed && parsed.state){ state = parsed.state; order = parsed.order || []; return true; }
      }catch(e){ console.warn('loadState error', e); }
      return false;
    }

    function loadSnapshot(){
      try{
        const raw = localStorage.getItem(SNAPSHOT_KEY);
        if(!raw) return null;
        return JSON.parse(raw);
      }catch(e){ console.warn('loadSnapshot error', e); return null; }
    }

    function updateLocalInfo(){
      const el = document.getElementById('local-info');
      const raw = localStorage.getItem(STORAGE_KEY);
      if(!raw) el.textContent = '';
      else{
        try{ const p = JSON.parse(raw); const d = new Date(p.timestamp); el.textContent = `Lần làm cuối: ${d.toLocaleString()}` }catch(e){ el.textContent = '' }
      }
    }

    // ---------- rendering ----------
    function render(){
      const qEl = document.getElementById('question');
      const answersEl = document.getElementById('answers');
      const explainEl = document.getElementById('explain');
      const progressEl = document.getElementById('progress');
      const scoreEl = document.getElementById('score');

      if(!workingQuestions.length){ qEl.textContent='Không có câu hỏi.'; answersEl.innerHTML=''; return }
      const idx = state.currentIndex;
      const qObj = workingQuestions[order[idx]];

      progressEl.textContent = `Câu ${idx+1} / ${workingQuestions.length}`;
      scoreEl.textContent = `Điểm: ${state.score}`;

      // animate question
      qEl.classList.remove('fade-in'); void qEl.offsetWidth; qEl.classList.add('fade-in');
      qEl.textContent = qObj.q;

      // answers
      answersEl.innerHTML='';
      qObj.choices.forEach((c,i)=>{
        const btn = document.createElement('button');
        btn.className='btn-answer fade-in';
        btn.type='button';
        btn.dataset.idx = i;
        btn.setAttribute('aria-label', `Đáp án ${String.fromCharCode(65+i)}: ${c}`);
        btn.innerHTML = `<div class="label">${String.fromCharCode(65+i)}</div><div class="text">${c}</div>`;
        btn.style.minHeight='56px';
        btn.addEventListener('click', onAnswer);

        // if already answered, show state
        const answeredKey = `${qObj.id}`;
        if(state.answered[answeredKey] !== undefined){
          const picked = state.answered[answeredKey];
          if(i === qObj.answer) btn.classList.add('correct');
          if(i === picked && picked !== qObj.answer) btn.classList.add('wrong');
          if(i === qObj.answer){ btn.style.boxShadow='0 10px 30px rgba(46,204,113,0.08)'; }
          btn.disabled = true;
        }

        answersEl.appendChild(btn);
      });

      // explanation area
      const answeredKey = `${qObj.id}`;
      if(state.answered[answeredKey] !== undefined){
        explainEl.textContent = qObj.explain || 'Không có lời giải.';
      } else explainEl.textContent = 'Chọn đáp án để xem kết quả và lời giải.';

      // buttons enable/disable
      document.getElementById('next').disabled = false;
      document.getElementById('prev').disabled = (state.currentIndex===0);
    }

    // ---------- handlers ----------
    function onAnswer(e){
      const btn = e.currentTarget;
      const choiceIdx = Number(btn.dataset.idx);
      const qObj = workingQuestions[order[state.currentIndex]];
      const key = `${qObj.id}`;
      if(state.answered[key] !== undefined) return; // already answered

      state.answered[key] = choiceIdx;
      if(choiceIdx === qObj.answer){ state.score += 1; }

      // update UI for all buttons (only change classes once)
      const answerButtons = Array.from(document.querySelectorAll('.btn-answer'));
      answerButtons.forEach(b=>{
        const i = Number(b.dataset.idx);
        b.disabled = true;
        if(i === qObj.answer) b.classList.add('correct');
        if(i === choiceIdx && i !== qObj.answer) b.classList.add('wrong');
        b.style.transition = 'transform .12s ease, box-shadow .12s ease';
      });

      document.getElementById('explain').textContent = qObj.explain || 'Không có lời giải.';
      saveState();
      // render() will pick up saved state on demand; keep a single render call
      render();
    }

    function goNext(){
      if(state.currentIndex < workingQuestions.length-1){ state.currentIndex +=1; saveState(); render(); }
      else{ // reached end -> show summary / offer restart
        alert(`Bạn đã hoàn tất. Điểm: ${state.score} / ${workingQuestions.length}`);
      }
    }
    function goPrev(){ if(state.currentIndex>0){ state.currentIndex -=1; saveState(); render(); } }

    function startNew(shuffleQuestions=true){
      // reset state
      state = { currentIndex:0, score:0, answered:{} };

      // create workingQuestions (deep copy) and shuffle choices only once here
      workingQuestions = deepCopy(originalQuestions);
      if(shuffleQuestions){
        workingQuestions = workingQuestions.map(q => shuffleChoicesForQuestion(q));
      }

      // create and shuffle order
      order = Array.from(Array(workingQuestions.length).keys());
      shuffle(order);

      saveState();
      render();
    }

    // ---------- load questions ----------
    async function loadQuestions(){
      // try to fetch external JSON (may fail on file:// URLs or CORS) - fallback to embedded
      try{
        const resp = await fetch(QUESTIONS_PATH, {cache: 'no-store'});
        if(!resp.ok) throw new Error('no file');
        const data = await resp.json();
        if(Array.isArray(data) && data.length) return data;
        throw new Error('invalid');
      }catch(e){
        console.warn('Falling back to embedded questions', e);
        return embeddedQuestions;
      }
    }

    // ---------- init ----------
    (async function(){
      originalQuestions = await loadQuestions();

      // ensure each question has an id and minimal validation
      originalQuestions = originalQuestions.map((q, idx)=>({ ...q, id: (q.id ?? (idx+1)) }));

      // try to restore snapshot (workingQuestions) and state
      const had = loadState();
      const snapshot = loadSnapshot();

      if(had && Array.isArray(snapshot) && snapshot.length === originalQuestions.length){
        // restore workingQuestions from snapshot (safe restore)
        workingQuestions = snapshot;
        // validate order length
        if(!order || order.length !== workingQuestions.length){ order = Array.from(Array(workingQuestions.length).keys()); shuffle(order); }
        render();
      } else {
        // first load or snapshot mismatch -> start fresh (shuffles choices + order)
        startNew(true);
      }

      // wire controls
      document.getElementById('restart').addEventListener('click', ()=>{ if(confirm('Làm lại và trộn lại toàn bộ câu hỏi?')) startNew(true); });
      document.getElementById('next').addEventListener('click', goNext);
      document.getElementById('prev').addEventListener('click', goPrev);

      // convenience: expose a reset function for developer console
      window._via_resetStorage = ()=>{ localStorage.removeItem(STORAGE_KEY); localStorage.removeItem(SNAPSHOT_KEY); alert('Đã xóa tiến trình. Tải lại trang.'); };

      updateLocalInfo();
    })();
  </script>
</body>
</html>
