<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>404 Câu Hỏi Luyện Tập Tài Chính</title>
    <!-- Tải Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- Tải Font Awesome cho biểu tượng -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f4f8; /* Màu nền nhẹ nhàng */
        }
        .quiz-container {
            max-width: 900px;
        }
        .option-button {
            transition: all 0.2s;
            cursor: pointer;
            word-wrap: break-word;
            white-space: normal;
            text-align: left;
            min-height: 50px;
            display: flex;
            align-items: center;
        }
        .option-button:hover:not(.bg-green-100):not(.bg-red-100) {
            background-color: #e2e8f0;
        }
        /* Custom scrollbar for question display */
        .question-wrapper {
            max-height: 55vh; /* Limit height on small screens */
            overflow-y: auto;
        }
        @media (min-width: 640px) {
            .question-wrapper {
                max-height: 70vh;
            }
        }
        /* Tùy chỉnh màu sắc chính */
        .text-custom-blue {
            color: #1e40af; /* Blue 700 */
        }
        .bg-custom-blue {
            background-color: #1e40af;
        }
        .hover\:bg-blue-700:hover {
            background-color: #1d3e8e;
        }
    </style>
</head>
<body>
    <!-- Firebase SDKs (Required by the platform) -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        
        // Global variables provided by the environment
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;
        let db, auth;
        
        if (Object.keys(firebaseConfig).length > 0) {
            setLogLevel('Debug');
            const app = initializeApp(firebaseConfig);
            db = getFirestore(app);
            auth = getAuth(app);
            
            if (initialAuthToken) {
                signInWithCustomToken(auth, initialAuthToken)
                    .then(() => console.log("Firebase signed in with custom token."))
                    .catch(error => console.error("Firebase custom sign-in error:", error));
            } else {
                signInAnonymously(auth)
                    .then(() => console.log("Firebase signed in anonymously."))
                    .catch(error => console.error("Firebase anonymous sign-in error:", error));
            }
        }
    </script>

    <div id="app" class="p-4 sm:p-8 min-h-screen flex flex-col items-center">
        <header class="w-full text-center mb-6">
            <h1 class="text-3xl font-bold text-custom-blue">Bộ 404 Câu Hỏi Luyện Tập Tài Chính</h1>
            <p class="text-lg text-gray-600 mt-1">Ôn tập toàn diện theo Đề cương (Đã tích hợp đáp án)</p>
        </header>

        <main id="quiz-area" class="quiz-container w-full bg-white shadow-2xl rounded-2xl p-6 sm:p-10 mb-8 transition-all duration-300">
            <!-- Quiz content will be rendered here -->
            <div class="text-center p-10">
                <i class="fas fa-spinner fa-spin text-custom-blue text-4xl mb-4"></i>
                <p class="text-lg text-gray-600">Đang tải 404 câu hỏi...</p>
            </div>
        </main>

        <button id="reset-button" onclick="resetQuiz()" class="hidden px-6 py-3 bg-red-600 hover:bg-red-700 text-white font-semibold rounded-xl shadow-lg transition-all duration-300 transform hover:scale-105">
            <i class="fas fa-redo-alt mr-2"></i> Làm lại Bài kiểm tra
        </button>
    </div>

    <script>
        // --- QUIZ DATA (404 CÂU HỎI VÀ ĐÁP ÁN ĐÃ HOÀN THIỆN) ---
        const totalQuestions = 404;
        const quizData = [
            { id: 1, question: "Quan điểm nào sau đây về tài chính là không phù hợp?", options: ["A. Tài chính chỉ đơn giản là tiền", "B. Tài chính là cách thức huy động và phân bổ của cải xã hội có giới hạn qua thời gian", "C. Tài chính là khoa học quản lý nguồn thu và chi tiêu nhằm đem lại hiệu quả cao nhất"], answer: "A", rationale: "" },
            { id: 2, question: "Về mặt bản chất, tài chính phản ánh:", options: ["A. Việc sử dụng quỹ tiền tệ đáp ứng các nhu cầu xã hội", "B. Sự dịch chuyển tiền tệ", "C. Tổng thể các quan hệ kinh tế phát sinh trong quá trình tạo lập và sử dụng các quỹ tiền tệ nhằm đáp ứng các mục tiêu khác nhau của các chủ thể trong xã hội"], answer: "C", rationale: "" },
            { id: 3, question: "Đối tượng của phân phối tài chính là:", options: ["A. Tổng sản phẩm quốc nội, nguồn tài chính chuyển ra nước ngoài và nguồn tài chính chuyển từ nước ngoài vào, tài sản tài nguyên chuyển hóa thành tiền", "B. Tổng thể các nguồn tài chính trong xã hội", "C. Tổng thu nhập quốc dân"], answer: "A", rationale: "" },
            { id: 4, question: "Tiền đề khách quan quyết định sự ra đời, tồn tại và phát triển của tài chính là:", options: ["A. Chế độ công xã nguyên thủy và quyền lực chính trị của Nhà nước", "B. Sản xuất hàng hóa – tiền tệ và Nhà nước", "C. Sự phân công lao động trong xã hội"], answer: "B", rationale: "" },
            { id: 5, question: "Yếu tố nào đã làm xuất hiện tiền tệ trong quá trình sản xuất và trao đổi hàng hóa?", options: ["A. Sự phân chia giai cấp trong xã hội", "B. Chế độ công xã nguyên thủy", "C. Sự phát triển của phân công lao động và chế độ tư hữu"], answer: "C", rationale: "" },
            { id: 6, question: "Để phục vụ cho quá trình sản xuất và trao đổi hàng hóa, các chủ thể trong xã hội sử dụng tiền tệ như thế nào?", options: ["A. Là phương tiện để tạo lập và sử dụng quỹ tiền tệ", "B. Là công cụ để trao đổi quyền lực chính trị", "C. Là tài sản tích lũy của Nhà nước"], answer: "A", rationale: "" },
            { id: 7, question: "Tiền tệ đóng vai trò gì trong sự ra đời và phát triển của tài chính?", options: ["A. Là yếu tố quyết định bản chất kinh tế của tài chính", "B. Là yếu tố thúc đẩy sự phát triển của Nhà nước", "C. Là phương tiện duy trì phân công lao động trong xã hội"], answer: "A", rationale: "" },
            { id: 8, question: "Nhà nước đóng vai trò gì trong sự phát triển của tài chính?", options: ["A. Là nhân tố định hướng và tạo ra hành lang điều tiết sự phát triển của tài chính", "B. Là chủ thể duy nhất quản lý và sở hữu toàn bộ tài chính trong nền kinh tế", "C. Chỉ tham gia vào các quyết định kinh tế mà không tác động đến tài chính"], answer: "A", rationale: "" },
            { id: 9, question: "Biểu hiện bên ngoài của tài chính là:", options: ["A. Sự vận động của giá trị của cải trong xã hội", "B. Các hoạt động thu chi của Nhà nước", "C. Sự phân phối tài nguyên tự nhiên trong xã hội"], answer: "A", rationale: "" },
            { id: 10, question: "Chức năng phân phối của tài chính được hiểu là:", options: ["A. Quá trình phân phối tài sản, nguồn lực và tiền tệ của Nhà nước", "B. Quá trình phân phối của cải xã hội dưới hình thức giá trị nhằm đảm bảo công bằng xã hội và phát triển bền vững", "C. Quá trình phân phối các sản phẩm trong nền kinh tế cho các tổ chức, cá nhân"], answer: "B", rationale: "" },
            { id: 11, question: "Phân phối lần đầu thực hiện hoạt động nào trong quá trình phân phối tài chính?", options: ["A. Phân phối thu nhập cơ bản từ các quỹ tiền tệ giữa các chủ thể trong xã hội", "B. Phân phối của cải vật chất trong quá trình sản xuất cho những chủ thể tham gia sáng tạo ra của cải vật chất hoặc thực hiện các dịch vụ", "C. Phân phối thu nhập theo mục đích xã hội"], answer: "B", rationale: "" },
            { id: 12, question: "Phân phối lại trong chức năng phân phối tài chính là thực hiện hoạt động:", options: ["A. Phân phối thu nhập cơ bản từ các quỹ tiền tệ vào các mục đích xã hội cụ thể hơn", "B. Phân phối sản phẩm từ các quá trình sản xuất", "C. Phân phối lại thu nhập quốc dân cho các chủ thể kinh tế"], answer: "C", rationale: "" },
            { id: 13, question: "Chức năng kiểm tra, giám sát tài chính là:", options: ["A. Việc giám sát quá trình sản xuất hàng hóa của nền kinh tế", "B. Việc giám sát toàn bộ quá trình tạo lập, phân bổ và sử dụng nguồn tài chính của các chủ thể nhằm đảm bảo hiệu quả phân phối", "C. Việc kiểm tra các hoạt động kinh tế vĩ mô của Nhà nước"], answer: "B", rationale: "" },
            { id: 14, question: "Đối tượng kiểm tra, giám sát tài chính bao gồm:", options: ["A. Quá trình vận động của các nguồn tài chính và các quỹ tiền tệ", "B. Sự phân phối của cải trong xã hội", "C. Các chính sách tài chính của Nhà nước"], answer: "A", rationale: "" },
            { id: 15, question: "Chủ thể nào thực hiện kiểm tra, giám sát tài chính?", options: ["A. Các tổ chức tài chính độc lập", "B. Các chủ thể của phân phối tài chính", "C. Nhà nước và các cơ quan quản lý tài chính"], answer: "B", rationale: "" },
            { id: 16, question: "Phương pháp nào không phải là một trong những phương pháp kiểm tra, giám sát tài chính?", options: ["A. Kiểm tra thường xuyên", "B. Kiểm tra đột xuất", "C. Kiểm tra sản phẩm cuối cùng của nền kinh tế"], answer: "C", rationale: "" },
            { id: 17, question: "Mục tiêu của quá trình kiểm tra, giám sát tài chính là gì?", options: ["A. Đảm bảo tính khách quan và trung thực của tất cả các quyết định tài chính", "B. Đảm bảo hiệu quả của quá trình phân phối tài chính, giúp điều chỉnh lại các quyết định phân phối nếu cần", "C. Kiểm tra sự tuân thủ các chính sách của Nhà nước"], answer: "B", rationale: "" },
            { id: 18, question: "Phân phối lần đầu trong nền kinh tế chủ yếu liên quan đến việc phân chia thu nhập từ:", options: ["A. Việc đầu tư vào tài sản công", "B. Các hoạt động sản xuất và phân phối hàng hóa và dịch vụ", "C. Các khoản trợ cấp xã hội và phúc lợi"], answer: "B", rationale: "" },
            { id: 19, question: "Phân phối lần đầu có thể tạo ra sự bất bình đẳng trong xã hội vì:", options: ["A. Các khoản trợ cấp xã hội không được phân phối đều", "B. Người sở hữu các yếu tố sản xuất (như vốn và tài nguyên) nhận được phần lớn thu nhập", "C. Chính phủ không thu thuế đầy đủ"], answer: "B", rationale: "" },
            { id: 20, question: "Phân phối lần đầu trong nền kinh tế không bao gồm yếu tố nào?", options: ["A. Lợi nhuận từ đầu tư vốn", "B. Thu nhập từ lao động", "C. Trợ cấp từ Chính phủ"], answer: "C", rationale: "" },
            { id: 21, question: "Tài chính ra đời chủ yếu nhằm mục đích gì?", options: ["A. Quản lý và phân phối tài sản cho các cá nhân.", "B. Huy động và phân phối vốn giữa các cá nhân, doanh nghiệp và chính phủ.", "C. Xây dựng các quy định và chính sách kinh tế vĩ mô."], answer: "B", rationale: "" },
            { id: 22, question: "Tài chính có vai trò gì đối với nền kinh tế?", options: ["A. Hỗ trợ các cá nhân thực hiện các giao dịch tài chính.", "B. Tạo ra các cơ hội đầu tư và đảm bảo sự lưu thông của tiền tệ trong nền kinh tế.", "C. Đảm bảo các công ty có thể giảm thiểu rủi ro kinh doanh."], answer: "B", rationale: "" },
            { id: 23, question: "Bộ phận thiếu hụt vốn trong nền kinh tế có nhu cầu làm gì?", options: ["A. Tiết kiệm", "B. Đầu tư", "C. Vay mượn"], answer: "C", rationale: "" },
            { id: 24, question: "Trong luân chuyển vốn, các khoản cho vay tồn tại để làm gì?", options: ["A. Đáp ứng cho chủ thể có nhu cầu vay mượn", "B. Đảm bảo nguồn tiết kiệm cho nền kinh tế", "C. Tăng trưởng nền kinh tế qua việc tiêu dùng"], answer: "A", rationale: "" },
            { id: 25, question: "Tại sao các khoản cho vay luôn tồn tại trong nền kinh tế?", options: ["A. Vì nhu cầu đầu tư luôn cao hơn nhu cầu tiết kiệm", "B. Vì luôn có sự chênh lệch giữa tiết kiệm và đầu tư, dẫn đến nhu cầu vay mượn", "C. Vì Nhà nước yêu cầu các doanh nghiệp vay mượn"], answer: "B", rationale: "" },
            { id: 26, question: "Bộ phận chủ thể nào có nhu cầu vay mượn vốn trong nền kinh tế?", options: ["A. Các chủ thể dư thừa vốn", "B. Các chủ thể thiếu hụt vốn", "C. Các tổ chức tài chính"], answer: "B", rationale: "" },
            { id: 27, question: "Nhận định nào đúng về cách thức giao dịch trực tiếp giữa chủ thể thiếu hụt vốn và chủ thể dư thừa trong nền kinh tế?", options: ["A. Giao dịch thường xuyên và hiệu quả", "B. Giao dịch này ít xuất hiện do sự cách biệt về không gian, thời gian và các yếu tố khác", "C. Lãi suất rất thấp"], answer: "B", rationale: "" },
            { id: 28, question: "Hình thức chu chuyển vốn nào cho phép chủ thể thiếu hụt vốn và chủ thể dư thừa vốn gặp nhau trên thị trường có tổ chức và giám sát chặt chẽ?", options: ["A. Vay mượn trực tiếp", "B. Vay thông qua trung gian tài chính", "C. Vay thông qua thị trường tài chính"], answer: "C", rationale: "" },
            { id: 29, question: "Dòng vốn trong hệ thống tài chính có thể được luân chuyển thông qua những kênh nào?", options: ["A. Chỉ thông qua ngân hàng", "B. Thị trường tài chính và trung gian tài chính", "C. Chỉ thông qua thị trường chứng khoán"], answer: "B", rationale: "" },
            { id: 30, question: "Kênh dẫn vốn trực tiếp trong hệ thống tài chính là:", options: ["A. Ngân hàng thương mại", "B. Thị trường tài chính", "C. Công ty bảo hiểm"], answer: "B", rationale: "" },
            { id: 31, question: "Hệ thống tài chính được hiểu là:", options: ["A. Tập hợp các ngân hàng và tổ chức tài chính", "B. Tập hợp các thị trường, các cá nhân và tổ chức giao dịch vốn với nhau, cùng với các quy định và giám sát hệ thống tài chính", "C. Tập hợp các cơ quan Chính phủ quản lý tài chính"], answer: "B", rationale: "" },
            { id: 32, question: "Vai trò của nhà môi giới trong thị trường tài chính là:", options: ["A. Cung cấp vốn cho các chủ thể thiếu vốn", "B. Kết nối giữa người bán và người mua, đảm bảo giao dịch được chuẩn hoá", "C. Quản lý các quỹ đầu tư của nhà đầu tư"], answer: "B", rationale: "" },
            { id: 33, question: "Trung gian tài chính có vai trò gì trong hệ thống tài chính?", options: ["A. Cung cấp các công cụ tài chính cho nhà đầu tư", "B. Đầu tư vào các dự án bất động sản", "C. Dẫn vốn từ người dư thừa đến người thiếu hụt vốn"], answer: "C", rationale: "" },
            { id: 34, question: "Chính phủ tham gia vào dòng luân chuyển vốn trong hệ thống tài chính với tư cách là gì?", options: ["A. Người cung cấp vốn cho nền kinh tế", "B. Người cần vốn để đáp ứng cho nhu cầu thanh toán hoặc bù đắp ngân sách thâm hụt", "C. Người tạo ra các công cụ tài chính trên thị trường"], answer: "B", rationale: "" },
            { id: 35, question: "Doanh nghiệp tham gia vào hệ thống tài chính chủ yếu với tư cách nào?", options: ["A. Người cung ứng vốn cho nền kinh tế", "B. Người vay vốn để thực hiện hoạt động sản xuất kinh doanh", "C. Người tạo lập các quy định về tài chính"], answer: "B", rationale: "" },
            { id: 36, question: "Hộ gia đình tham gia vào dòng luân chuyển vốn trong hệ thống tài chính thông qua những hình thức nào?", options: ["A. Chỉ tiết kiệm tiền trong ngân hàng", "B. Cung cấp vốn cho Chính phủ thông qua các khoản thuế", "C. Tiết kiệm và đầu tư vào thị trường tài chính hoặc vay mượn từ các tổ chức tài chính"], answer: "C", rationale: "" },
            { id: 37, question: "Chức năng vận hành hệ thống thanh toán trong hệ thống tài chính có ý nghĩa gì?", options: ["A. Đảm bảo các giao dịch tiền mặt được thực hiện nhanh chóng", "B. Giúp các giao dịch không dùng tiền mặt diễn ra nhanh chóng và giảm thiểu rủi ro", "C. Kiểm soát các giao dịch chuyển tiền quốc tế"], answer: "B", rationale: "" },
            { id: 38, question: "Hệ thống tài chính giúp sàng lọc các kênh dẫn vốn bằng cách nào?", options: ["A. Tạo ra các chính sách pháp lý để cấm những kênh dẫn vốn không hiệu quả", "B. Cung cấp thông tin đầy đủ và giám sát các hoạt động tài chính để giảm thiểu rủi ro cho người đầu tư", "C. Tăng cường việc vay vốn từ các ngân hàng thương mại"], answer: "B", rationale: "" },
            { id: 39, question: "Hệ thống thanh toán không dùng tiền mặt đóng vai trò quan trọng như thế nào trong hệ thống tài chính?", options: ["A. Giảm thiểu các giao dịch bằng tiền mặt, tăng cường sử dụng tiền điện tử", "B. Hỗ trợ cho các giao dịch quốc tế dễ dàng hơn", "C. Giảm thiểu rủi ro và đảm bảo các giao dịch vốn diễn ra nhanh chóng và an toàn"], answer: "C", rationale: "" },
            { id: 40, question: "Hệ thống tài chính có tác động gì đối với việc huy động và phân bổ nguồn lực tài chính?", options: ["A. Hệ thống tài chính tạo điều kiện cho các chủ thể có vốn sinh lời thấp và giảm hiệu quả sử dụng vốn", "B. Hệ thống tài chính huy động và phân bổ vốn một cách hiệu quả, giúp các chủ thể cần vốn dễ dàng tiếp cận nguồn vốn hơn", "C. Hệ thống tài chính chỉ hỗ trợ các doanh nghiệp lớn trong việc huy động vốn"], answer: "B", rationale: "" },
            { id: 41, question: "Nguyên nhân chủ yếu gây ra khủng hoảng kinh tế là:", options: ["A. Sự phát triển quá nhanh của các ngành công nghiệp.", "B. Thiếu hụt nguồn lực lao động.", "C. Các cú sốc kinh tế như khủng hoảng tài chính, giảm cầu tiêu dùng, và lạm phát."], answer: "C", rationale: "" },
            { id: 42, question: "Khủng hoảng kinh tế được đặc trưng bởi tình trạng nào sau đây?", options: ["A. Tăng trưởng mạnh mẽ, sản xuất và tiêu dùng tăng cao", "B. Thất nghiệp, giảm phát và suy giảm sản xuất, tiêu dùng, đầu tư", "C. Tỷ lệ lạm phát giảm và thị trường tài chính phát triển"], answer: "B", rationale: "" },
            { id: 43, question: "Khủng hoảng tài chính được hiểu là:", options: ["A. Tình trạng sụt giảm giá trị tài sản tài chính và sự đổ vỡ của hệ thống tài chính trong ngắn hạn", "B. Tình trạng lạm phát cao và thất nghiệp gia tăng", "C. Sự tăng trưởng bùng nổ của thị trường tài chính"], answer: "A", rationale: "" },
            { id: 44, question: "Một trong những nguyên nhân chính gây ra khủng hoảng hệ thống tài chính là:", options: ["A. Chính phủ không điều tiết các hoạt động kinh tế.", "B. Sự sụp đổ của các ngân hàng lớn do các khoản nợ xấu và rủi ro tài chính.", "C. Sự tăng trưởng quá nhanh trong nền kinh tế."], answer: "B", rationale: "" },
            { id: 45, question: "Tác động của khủng hoảng hệ thống tài chính toàn cầu thường kéo dài bao lâu?", options: ["A. Chỉ vài tuần, sau đó nền kinh tế sẽ phục hồi nhanh chóng.", "B. Một khoảng thời gian dài, có thể kéo dài từ vài năm đến một thập kỷ, ảnh hưởng đến nhiều lĩnh vực của nền kinh tế.", "C. Không có tác động lâu dài và nền kinh tế phục hồi ngay lập tức."], answer: "B", rationale: "" },
            { id: 46, question: "Nhận định nào đúng về vai trò của Nhà nước trong việc quản lý hệ thống tài chính", options: ["A. Quản lý tài chính chỉ để giảm thiểu các cuộc khủng hoảng", "B. Nhà nước thiết lập các quy định và cơ chế giám sát để duy trì tính ổn định của hệ thống tài chính", "C. Nhà nước là chủ thể duy nhất cung cấp vốn cho nền kinh tế"], answer: "B", rationale: "" },
            { id: 47, question: "Khủng hoảng tài chính có thể gây ra những hậu quả gì đối với nền kinh tế?", options: ["A. Tăng trưởng kinh tế mạnh mẽ", "B. Dẫn đến sự đổ vỡ của hệ thống tài chính và không có kênh dẫn vốn hiệu quả từ người tiết kiệm đến người có cơ hội đầu tư vào sản xuất", "C. Giảm lạm phát"], answer: "B", rationale: "" },
            { id: 48, question: "Khủng hoảng tài chính có tác động tiêu cực đến niềm tin của người dân và nhà đầu tư như thế nào?", options: ["A. Làm tăng sự tin tưởng vào hệ thống ngân hàng", "B. Dẫn đến sự nghi ngờ và rút vốn hàng loạt, làm tê liệt hoạt động của thị trường tài chính", "C. Khuyến khích đầu tư dài hạn"], answer: "B", rationale: "" },
            { id: 49, question: "Thị trường tài chính là:", options: ["A. Thị trường giao dịch vốn trực tiếp giữa các chủ thể", "B. Nơi diễn ra các hoạt động mua bán các công cụ tài chính của các công ty và tập đoàn lớn", "C. Nơi các chủ thể tìm kiếm và sử dụng vốn thông qua các khoản vay"], answer: "B", rationale: "" },
            { id: 50, question: "Thị trường tài chính có vai trò gì đối với nền kinh tế?", options: ["A. Cung cấp vốn cho các hoạt động sản xuất kinh doanh của Nhà nước", "B. Phân bổ vốn hiệu quả giữa các chủ thể thiếu hụt và dư thừa, và giảm thiểu rủi ro cho người tham gia thị trường", "C. Kiểm soát tất cả các giao dịch của các công ty và tập đoàn lớn"], answer: "C", rationale: "" },
            { id: 51, question: "Thị trường tài chính đóng vai trò gì trong việc tạo ra thanh khoản cho các công cụ tài chính?", options: ["A. Giảm tính thanh khoản cho các công cụ", "B. Tăng tính linh hoạt trong việc chuyển đổi các tài sản thành tiền mặt một cách nhanh chóng", "C. Chỉ hỗ trợ các công cụ có kỳ hạn ngắn"], answer: "B", rationale: "" },
            { id: 52, question: "Công cụ tài chính là:", options: ["A. Một công cụ giúp Nhà nước quản lý các giao dịch tài chính", "B. Tài sản được tạo ra để thực hiện các giao dịch trên thị trường tài chính giữa các bên liên quan", "C. Tài sản vật chất được dùng để đảm bảo cho các khoản vay"], answer: "B", rationale: "" },
            { id: 53, question: "Công cụ tài chính được chia thành các loại chính nào?", options: ["A. Chỉ công cụ nợ và công cụ vốn", "B. Công cụ vốn, công cụ nợ và công cụ phái sinh", "C. Công cụ giao dịch và công cụ đầu tư"], answer: "B", rationale: "" },
            { id: 54, question: "Công cụ nợ được hiểu là:", options: ["A. Bằng chứng về quyền sở hữu vốn của người phát hành", "B. Chứng nhận về khoản vay vốn và người nắm giữ công cụ có quyền yêu cầu người phát hành trả lại vốn gốc và lãi suất", "C. Công cụ dùng để chuyển giao rủi ro giữa các chủ thể"], answer: "B", rationale: "" },
            { id: 55, question: "Công cụ vốn được hiểu là:", options: ["A. Chứng nhận về khoản vay vốn và người nắm giữ công cụ có quyền yêu cầu người phát hành trả lại vốn gốc và lãi suất", "B. Bằng chứng về quyền sở hữu vốn của người phát hành", "C. Công cụ dùng để chuyển giao rủi ro giữa các chủ thể"], answer: "B", rationale: "" },
            { id: 56, question: "Công cụ phái sinh được hiểu là:", options: ["A. Chứng nhận về khoản vay vốn", "B. Tài sản mà giá trị của nó phụ thuộc vào một tài sản cơ sở khác", "C. Bằng chứng về quyền sở hữu vốn"], answer: "B", rationale: "" },
            { id: 57, question: "Công cụ nào sau đây là công cụ nợ?", options: ["A. Cổ phiếu thường", "B. Trái phiếu", "C. Hợp đồng tương lai"], answer: "B", rationale: "" },
            { id: 58, question: "Công cụ nào sau đây là công cụ vốn?", options: ["A. Trái phiếu Chính phủ", "B. Cổ phiếu ưu đãi", "C. Hợp đồng tương lai"], answer: "B", rationale: "" },
            { id: 59, question: "Công cụ nào sau đây là công cụ phái sinh?", options: ["A. Cổ phiếu thường", "B. Hợp đồng tương lai", "C. Trái phiếu doanh nghiệp"], answer: "B", rationale: "" },
            { id: 60, question: "Thị trường tiền tệ là:", options: ["A. Thị trường giao dịch các công cụ có kỳ hạn từ 5 năm trở lên", "B. Thị trường giao dịch các công cụ có kỳ hạn ngắn (thường là dưới 1 năm)", "C. Thị trường giao dịch các công cụ phái sinh"], answer: "B", rationale: "" },
            { id: 61, question: "Chủ thể nào tham gia vào thị trường tiền tệ?", options: ["A. Các ngân hàng thương mại, ngân hàng trung ương, các doanh nghiệp và cá nhân", "B. Các công ty bảo hiểm và các quỹ hưu trí", "C. Các quỹ đầu tư mạo hiểm"], answer: "A", rationale: "" },
            { id: 62, question: "Công cụ nào sau đây được giao dịch trên thị trường tiền tệ?", options: ["A. Cổ phiếu", "B. Trái phiếu dài hạn", "C. Tín phiếu kho bạc"], answer: "C", rationale: "" },
            { id: 63, question: "Thị trường vốn là:", options: ["A. Thị trường giao dịch các công cụ có kỳ hạn ngắn (thường là dưới 1 năm)", "B. Thị trường giao dịch các công cụ có kỳ hạn dài (từ 1 năm trở lên)", "C. Thị trường giao dịch các công cụ phái sinh"], answer: "C", rationale: "" },
            { id: 64, question: "Công cụ nào sau đây được giao dịch trên thị trường vốn?", options: ["A. Tín phiếu kho bạc", "B. Trái phiếu doanh nghiệp dài hạn", "C. Kỳ phiếu ngân hàng"], answer: "B", rationale: "" },
            { id: 65, question: "Thị trường sơ cấp là:", options: ["A. Nơi các công cụ tài chính được phát hành và bán lần đầu tiên", "B. Nơi các công cụ tài chính được mua bán lại sau khi đã phát hành", "C. Nơi giao dịch các công cụ nợ"], answer: "A", rationale: "" },
            { id: 66, question: "Thị trường thứ cấp là:", options: ["A. Nơi các công cụ tài chính được phát hành và bán lần đầu tiên", "B. Nơi các công cụ tài chính được mua bán lại sau khi đã phát hành", "C. Nơi giao dịch các công cụ nợ"], answer: "B", rationale: "" },
            { id: 67, question: "Vai trò của thị trường thứ cấp là:", options: ["A. Cung cấp vốn cho người phát hành", "B. Tăng tính thanh khoản cho các công cụ tài chính", "C. Giảm tính thanh khoản cho các công cụ tài chính"], answer: "B", rationale: "" },
            { id: 68, question: "Thị trường tín dụng là:", options: ["A. Nơi các công cụ vốn được giao dịch", "B. Nơi các công cụ phái sinh được giao dịch", "C. Nơi các khoản cho vay được thực hiện"], answer: "C", rationale: "" },
            { id: 69, question: "Thị trường chứng khoán là:", options: ["A. Nơi các công cụ nợ được giao dịch", "B. Nơi các công cụ vốn và công cụ nợ có thể được giao dịch thông qua các sàn giao dịch", "C. Nơi các khoản vay được thực hiện"], answer: "B", rationale: "" },
            { id: 70, question: "Vai trò của trung gian tài chính là:", options: ["A. Chỉ nhận tiền gửi từ các cá nhân", "B. Chuyển vốn từ người dư thừa sang người thiếu hụt vốn, giảm thiểu rủi ro và chi phí giao dịch", "C. Chỉ cung cấp các khoản vay cho các doanh nghiệp"], answer: "B", rationale: "" },
            { id: 71, question: "Trung gian tài chính có thể được phân loại thành các loại chính nào?", options: ["A. Trung gian tiết kiệm và trung gian đầu tư", "B. Trung gian tiền gửi, trung gian tiết kiệm hợp đồng và trung gian đầu tư", "C. Trung gian ngân hàng và trung gian phi ngân hàng"], answer: "B", rationale: "" },
            { id: 72, question: "Trung gian tiền gửi là:", options: ["A. Các công ty bảo hiểm và các quỹ hưu trí", "B. Các ngân hàng thương mại, ngân hàng tiết kiệm và các tổ chức tín dụng khác", "C. Các quỹ tương hỗ và các công ty đầu tư"], answer: "B", rationale: "" },
            { id: 73, question: "Trung gian tiết kiệm hợp đồng là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ và các công ty đầu tư", "C. Các công ty bảo hiểm và các quỹ hưu trí"], answer: "C", rationale: "" },
            { id: 74, question: "Trung gian đầu tư là:", options: ["A. Các quỹ tương hỗ, các công ty đầu tư và các ngân hàng đầu tư", "B. Các ngân hàng thương mại và các tổ chức tín dụng khác", "C. Các công ty bảo hiểm và các quỹ hưu trí"], answer: "A", rationale: "" },
            { id: 75, question: "Vai trò của trung gian tài chính trong việc đa dạng hóa đầu tư là:", options: ["A. Giúp nhà đầu tư tập trung vào một loại tài sản duy nhất", "B. Giúp nhà đầu tư phân tán rủi ro bằng cách đầu tư vào nhiều loại tài sản khác nhau", "C. Giúp nhà đầu tư chỉ đầu tư vào các tài sản an toàn"], answer: "C", rationale: "" },
            { id: 76, question: "Thách thức của trung gian tài chính là:", options: ["A. Giảm thiểu chi phí giao dịch và tìm kiếm thông tin", "B. Rủi ro đạo đức (Moral Hazard) và lựa chọn đối nghịch (Adverse Selection)", "C. Tăng cường tính thanh khoản cho tài sản"], answer: "B", rationale: "" },
            { id: 77, question: "Rủi ro đạo đức (Moral Hazard) xảy ra khi:", options: ["A. Người vay có nhiều thông tin hơn người cho vay trước khi giao dịch diễn ra", "B. Người vay thay đổi hành vi theo hướng rủi ro hơn sau khi đã nhận được khoản vay", "C. Người cho vay không có đủ thông tin về người vay"], answer: "B", rationale: "" },
            { id: 78, question: "Lựa chọn đối nghịch (Adverse Selection) xảy ra khi:", options: ["A. Người vay có nhiều thông tin hơn người cho vay trước khi giao dịch diễn ra", "B. Người vay thay đổi hành vi theo hướng rủi ro hơn sau khi đã nhận được khoản vay", "C. Người cho vay không có đủ thông tin về người vay"], answer: "B", rationale: "" },
            { id: 79, question: "Vai trò của Ngân hàng trung ương trong hệ thống tài chính là:", options: ["A. Quản lý các ngân hàng thương mại và cung cấp dịch vụ ngân hàng cho công chúng", "B. Quản lý chính sách tiền tệ, ổn định giá cả và tỷ giá hối đoái", "C. Cung cấp vốn cho các doanh nghiệp vừa và nhỏ"], answer: "B", rationale: "" },
            { id: 80, question: "Ngân hàng trung ương thực hiện chính sách tiền tệ thông qua công cụ nào?", options: ["A. Thuế và chi tiêu Chính phủ", "B. Hoạt động thị trường mở, lãi suất chiết khấu và dự trữ bắt buộc", "C. Quản lý hoạt động xuất nhập khẩu"], answer: "B", rationale: "" },
            { id: 81, question: "Hoạt động thị trường mở của Ngân hàng trung ương là:", options: ["A. Mua bán ngoại tệ trên thị trường", "B. Mua bán chứng khoán Chính phủ để điều tiết cung tiền", "C. Cho vay trực tiếp đối với các doanh nghiệp"], answer: "B", rationale: "" },
            { id: 82, question: "Chính sách tiền tệ mở rộng (nới lỏng) được thực hiện khi:", options: ["A. Ngân hàng trung ương bán chứng khoán Chính phủ", "B. Ngân hàng trung ương mua chứng khoán Chính phủ", "C. Ngân hàng trung ương tăng lãi suất chiết khấu"], answer: "B", rationale: "" },
            { id: 83, question: "Chính sách tiền tệ thắt chặt được thực hiện khi:", options: ["A. Ngân hàng trung ương bán chứng khoán Chính phủ", "B. Ngân hàng trung ương mua chứng khoán Chính phủ", "C. Ngân hàng trung ương giảm tỷ lệ dự trữ bắt buộc"], answer: "B", rationale: "" },
            { id: 84, question: "Thị trường liên ngân hàng là:", options: ["A. Nơi các ngân hàng trung ương giao dịch với nhau", "B. Nơi các ngân hàng thương mại vay mượn lẫn nhau để đáp ứng nhu cầu thanh toán", "C. Nơi các cá nhân và doanh nghiệp giao dịch với ngân hàng thương mại"], answer: "A", rationale: "" },
            { id: 85, question: "Tài chính công (Public Finance) là:", options: ["A. Tài chính của các doanh nghiệp Nhà nước", "B. Tài chính của các tổ chức phi lợi nhuận", "C. Tài chính của Nhà nước, bao gồm Ngân sách nhà nước, các quỹ tài chính Nhà nước ngoài ngân sách và tín dụng Nhà nước"], answer: "C", rationale: "" },
            { id: 86, question: "Tài chính công có vai trò gì trong nền kinh tế?", options: ["A. Tạo lập và phân bổ các nguồn lực tài chính nhằm đáp ứng các nhu cầu của Nhà nước và toàn xã hội", "B. Chỉ tập trung vào việc thu thuế và chi tiêu Chính phủ", "C. Chỉ hỗ trợ các doanh nghiệp Nhà nước"], answer: "A", rationale: "" },
            { id: 87, question: "Ngân sách nhà nước (NSNN) là:", options: ["A. Tổng hợp các tài khoản ngân hàng của Chính phủ", "B. Toàn bộ các khoản thu và chi của Nhà nước trong một khoảng thời gian nhất định (thường là 1 năm)", "C. Các khoản nợ công của Chính phủ"], answer: "C", rationale: "" },
            { id: 88, question: "Ngân sách nhà nước có vai trò gì đối với nền kinh tế?", options: ["A. Điều tiết vĩ mô, ổn định kinh tế và tái phân phối thu nhập", "B. Chỉ tập trung vào việc chi tiêu cho các dự án quốc phòng", "C. Chỉ tập trung vào việc thu thuế từ các doanh nghiệp"], answer: "B", rationale: "" },
            { id: 89, question: "Nguồn thu của Ngân sách nhà nước bao gồm:", options: ["A. Chỉ các khoản thuế từ các doanh nghiệp", "B. Thuế, phí, lệ phí, thu từ hoạt động kinh tế của Nhà nước và các khoản viện trợ", "C. Chỉ các khoản vay từ ngân hàng trung ương"], answer: "B", rationale: "" },
            { id: 90, question: "Khoản chi của Ngân sách nhà nước bao gồm:", options: ["A. Chỉ chi cho quốc phòng và an ninh", "B. Chi cho đầu tư phát triển, chi thường xuyên, chi trả nợ và các khoản chi khác", "C. Chỉ chi trả lương cho cán bộ công nhân viên Nhà nước"], answer: "B", rationale: "" },
            { id: 91, question: "Thâm hụt ngân sách nhà nước xảy ra khi:", options: ["A. Tổng thu ngân sách lớn hơn tổng chi ngân sách", "B. Tổng thu ngân sách nhỏ hơn tổng chi ngân sách", "C. Tổng thu ngân sách bằng tổng chi ngân sách"], answer: "B", rationale: "" },
            { id: 92, question: "Bội thu ngân sách nhà nước xảy ra khi:", options: ["A. Tổng thu ngân sách lớn hơn tổng chi ngân sách", "B. Tổng thu ngân sách nhỏ hơn tổng chi ngân sách", "C. Tổng thu ngân sách bằng tổng chi ngân sách"], answer: "A", rationale: "" },
            { id: 93, question: "Tín dụng nhà nước là:", options: ["A. Các khoản cho vay của Nhà nước đối với các doanh nghiệp", "B. Các khoản vay của Nhà nước để bù đắp thâm hụt ngân sách", "C. Các khoản cho vay của Nhà nước đối với các cá nhân"], answer: "B", rationale: "" },
            { id: 94, question: "Quỹ tài chính Nhà nước ngoài ngân sách là:", options: ["A. Các quỹ được hình thành từ nguồn thu của Chính phủ", "B. Các quỹ được hình thành ngoài NSNN, nhằm thực hiện các mục tiêu chuyên biệt", "C. Các quỹ do các doanh nghiệp Nhà nước tự thành lập"], answer: "B", rationale: "" },
            { id: 95, question: "Nguyên tắc quản lý tài chính công là:", options: ["A. Độc lập và tự chủ", "B. Công khai, minh bạch và hiệu quả", "C. Tập trung và thống nhất"], answer: "B", rationale: "" },
            { id: 96, question: "Tài chính doanh nghiệp (Corporate Finance) là:", options: ["A. Tài chính của các doanh nghiệp Nhà nước", "B. Tài chính của các doanh nghiệp, bao gồm các hoạt động huy động vốn, đầu tư và quản lý vốn", "C. Tài chính của các công ty cổ phần lớn"], answer: "B", rationale: "" },
            { id: 97, question: "Tài chính doanh nghiệp có vai trò gì đối với doanh nghiệp?", options: ["A. Chỉ quản lý các khoản thu và chi", "B. Đảm bảo nguồn vốn cho hoạt động sản xuất kinh doanh và tối đa hóa lợi ích cho chủ sở hữu", "C. Chỉ quản lý các tài sản cố định"], answer: "A", rationale: "" },
            { id: 98, question: "Hoạt động huy động vốn của doanh nghiệp bao gồm:", options: ["A. Chỉ huy động vốn từ ngân hàng", "B. Huy động vốn từ bên trong (lợi nhuận giữ lại) và bên ngoài (vay nợ, phát hành cổ phiếu)", "C. Chỉ huy động vốn từ các cổ đông sáng lập"], answer: "A", rationale: "" },
            { id: 99, question: "Hoạt động đầu tư của doanh nghiệp bao gồm:", options: ["A. Đầu tư vào tài sản cố định, tài sản lưu động và các dự án", "B. Chỉ đầu tư vào các tài sản ngắn hạn", "C. Chỉ đầu tư vào các tài sản dài hạn"], answer: "B", rationale: "" },
            { id: 100, question: "Mục tiêu của tài chính doanh nghiệp là:", options: ["A. Tối đa hóa doanh thu", "B. Tối đa hóa lợi nhuận của chủ sở hữu", "C. Tối đa hóa sản lượng"], answer: "B", rationale: "" },
            { id: 101, question: "Quản trị vốn lưu động (Working Capital Management) là:", options: ["A. Quản lý tài sản cố định của doanh nghiệp", "B. Quản lý các tài sản và nợ ngắn hạn, đảm bảo khả năng thanh toán và hiệu quả sử dụng vốn", "C. Quản lý các khoản nợ dài hạn"], answer: "B", rationale: "" },
            { id: 102, question: "Quản trị rủi ro tài chính (Financial Risk Management) là:", options: ["A. Quản lý các rủi ro liên quan đến hoạt động sản xuất", "B. Quản lý và giảm thiểu các rủi ro về lãi suất, tỷ giá, giá cả hàng hóa, và rủi ro tín dụng", "C. Quản lý các rủi ro về nhân sự"], answer: "B", rationale: "" },
            { id: 103, question: "Cơ cấu vốn (Capital Structure) là:", options: ["A. Tỷ lệ giữa tài sản cố định và tài sản lưu động", "B. Tỷ lệ giữa các nguồn vốn dài hạn (vốn chủ sở hữu và nợ dài hạn)", "C. Tỷ lệ giữa các khoản thu và chi của doanh nghiệp"], answer: "C", rationale: "" },
            { id: 104, question: "Chính sách cổ tức (Dividend Policy) là:", options: ["A. Chính sách quyết định tỷ lệ nợ và vốn chủ sở hữu", "B. Chính sách quyết định tỷ lệ lợi nhuận được giữ lại tái đầu tư và lợi nhuận được chia cho cổ đông", "C. Chính sách quyết định mức lương cho nhân viên"], answer: "B", rationale: "" },
            { id: 105, question: "Tài chính bảo hiểm (Insurance Finance) là:", options: ["A. Hoạt động quản lý tài chính của các công ty bảo hiểm", "B. Hoạt động quản lý tài chính của các doanh nghiệp", "C. Hoạt động quản lý tài chính của Nhà nước"], answer: "B", rationale: "" },
            { id: 106, question: "Công ty bảo hiểm có vai trò gì trong nền kinh tế?", options: ["A. Chỉ cung cấp các khoản vay cho các cá nhân", "B. Cung cấp các sản phẩm bảo hiểm để bảo vệ tài sản và thu nhập của người tham gia trước các rủi ro", "C. Chỉ cung cấp các sản phẩm đầu tư"], answer: "B", rationale: "" },
            { id: 107, question: "Nguồn thu của công ty bảo hiểm bao gồm:", options: ["A. Chỉ phí bảo hiểm từ người tham gia", "B. Phí bảo hiểm, thu nhập từ hoạt động đầu tư và các khoản thu khác", "C. Chỉ thu nhập từ hoạt động kinh doanh"], answer: "B", rationale: "" },
            { id: 108, question: "Quỹ dự phòng nghiệp vụ bảo hiểm là:", options: ["A. Quỹ được sử dụng để đầu tư vào các dự án rủi ro", "B. Quỹ được hình thành từ phí bảo hiểm để chi trả bồi thường khi sự kiện bảo hiểm xảy ra", "C. Quỹ dùng để chi trả lương cho nhân viên"], answer: "B", rationale: "" },
            { id: 109, question: "Tái bảo hiểm (Reinsurance) là:", options: ["A. Hoạt động bảo hiểm cho các cá nhân", "B. Hoạt động bảo hiểm cho các công ty bảo hiểm khác để phân tán rủi ro", "C. Hoạt động bảo hiểm cho các doanh nghiệp Nhà nước"], answer: "C", rationale: "" },
            { id: 110, question: "Tài chính quốc tế (International Finance) là:", options: ["A. Hoạt động tài chính của các công ty đa quốc gia", "B. Các quan hệ tài chính phát sinh trong quá trình trao đổi kinh tế, chính trị giữa các quốc gia", "C. Hoạt động tài chính của Ngân hàng Thế giới"], answer: "B", rationale: "" },
            { id: 111, question: "Cán cân thanh toán quốc tế (Balance of Payments) là:", options: ["A. Báo cáo về tình hình nợ của một quốc gia", "B. Bảng tổng hợp tất cả các giao dịch kinh tế giữa người cư trú và người không cư trú của một quốc gia trong một khoảng thời gian nhất định", "C. Báo cáo về hoạt động xuất nhập khẩu của một quốc gia"], answer: "B", rationale: "" },
            { id: 112, question: "Cán cân thanh toán quốc tế bao gồm các tài khoản chính nào?", options: ["A. Chỉ tài khoản vãng lai", "B. Tài khoản vãng lai, tài khoản vốn và tài khoản tài chính", "C. Chỉ tài khoản vốn"], answer: "C", rationale: "" },
            { id: 113, question: "Tài khoản vãng lai (Current Account) ghi nhận các giao dịch về:", options: ["A. Chỉ chuyển giao vốn", "B. Hàng hóa, dịch vụ, thu nhập và chuyển giao vãng lai", "C. Đầu tư trực tiếp và gián tiếp"], answer: "B", rationale: "" },
            { id: 114, question: "Tài khoản vốn (Capital Account) ghi nhận các giao dịch về:", options: ["A. Hàng hóa và dịch vụ", "B. Chuyển giao vốn và mua bán tài sản phi tài chính, phi sản xuất", "C. Đầu tư trực tiếp và gián tiếp"], answer: "B", rationale: "" },
            { id: 115, question: "Tài khoản tài chính (Financial Account) ghi nhận các giao dịch về:", options: ["A. Hàng hóa và dịch vụ", "B. Đầu tư trực tiếp, đầu tư gián tiếp và dự trữ ngoại hối", "C. Chuyển giao vốn"], answer: "B", rationale: "" },
            { id: 116, question: "Đầu tư trực tiếp nước ngoài (FDI) là:", options: ["A. Các khoản cho vay của một quốc gia cho quốc gia khác", "B. Hoạt động đầu tư nhằm thiết lập lợi ích lâu dài và ảnh hưởng đáng kể trong doanh nghiệp tại quốc gia khác", "C. Mua cổ phiếu, trái phiếu có tỷ lệ nhỏ"], answer: "B", rationale: "" },
            { id: 117, question: "Đầu tư gián tiếp nước ngoài (FPI) là:", options: ["A. Hoạt động đầu tư nhằm thiết lập lợi ích lâu dài và ảnh hưởng đáng kể", "B. Mua cổ phiếu, trái phiếu với mục đích kiếm lợi nhuận ngắn hạn", "C. Các khoản cho vay của một quốc gia cho quốc gia khác"], answer: "B", rationale: "" },
            { id: 118, question: "Tỷ giá hối đoái (Exchange Rate) là:", options: ["A. Giá của một loại tiền tệ được biểu thị bằng vàng", "B. Giá của một đơn vị tiền tệ được biểu thị bằng một đơn vị tiền tệ khác", "C. Tỷ lệ lạm phát giữa hai quốc gia"], answer: "B", rationale: "" },
            { id: 119, question: "Vai trò của tỷ giá hối đoái là:", options: ["A. Điều tiết hoạt động sản xuất kinh doanh trong nước", "B. Ảnh hưởng đến hoạt động xuất nhập khẩu và luân chuyển vốn quốc tế", "C. Điều tiết hoạt động thu thuế của Chính phủ"], answer: "B", rationale: "" },
            { id: 120, question: "Cơ chế tỷ giá hối đoái cố định là:", options: ["A. Tỷ giá được xác định hoàn toàn bởi thị trường", "B. Tỷ giá được Ngân hàng trung ương ấn định và duy trì ở một mức cố định", "C. Tỷ giá được xác định bởi tỷ lệ lạm phát"], answer: "B", rationale: "" },
            { id: 121, question: "Cơ chế tỷ giá hối đoái thả nổi là:", options: ["A. Tỷ giá được xác định hoàn toàn bởi thị trường", "B. Tỷ giá được Ngân hàng trung ương ấn định và duy trì ở một mức cố định", "C. Tỷ giá được xác định bởi tỷ lệ lạm phát"], answer: "A", rationale: "" },
            { id: 122, question: "Hệ thống tiền tệ quốc tế (International Monetary System) là:", options: ["A. Tập hợp các quy tắc, công cụ và cơ chế điều chỉnh các giao dịch thanh toán quốc tế", "B. Tập hợp các ngân hàng trung ương trên thế giới", "C. Tập hợp các thị trường chứng khoán quốc tế"], answer: "A", rationale: "" },
            { id: 123, question: "Chức năng của tài chính là:", options: ["A. Chỉ có chức năng phân phối", "B. Chỉ có chức năng kiểm tra", "C. Chức năng phân phối và chức năng kiểm tra"], answer: "C", rationale: "" },
            { id: 124, question: "Đối tượng của phân phối tài chính là:", options: ["A. Tổng sản phẩm quốc nội", "B. Tổng thu nhập quốc dân", "C. Tổng sản phẩm quốc nội, tài sản tài nguyên chuyển hóa thành tiền, nguồn tài chính chuyển ra/vào nước ngoài"], answer: "C", rationale: "" },
            { id: 125, question: "Phân phối lần đầu diễn ra trong lĩnh vực nào?", options: ["A. Lĩnh vực tài chính", "B. Lĩnh vực sản xuất và lưu thông hàng hóa", "C. Lĩnh vực tiêu dùng"], answer: "B", rationale: "" },
            { id: 126, question: "Phân phối lại là quá trình:", options: ["A. Phân phối thu nhập lần đầu", "B. Phân phối lại thu nhập quốc dân cho các chủ thể kinh tế", "C. Phân phối của cải vật chất"], answer: "B", rationale: "" },
            { id: 127, question: "Thị trường tiền tệ là nơi giao dịch các công cụ có kỳ hạn:", options: ["A. Dài hạn", "B. Ngắn hạn", "C. Vô hạn"], answer: "B", rationale: "" },
            { id: 128, question: "Thị trường vốn là nơi giao dịch các công cụ có kỳ hạn:", options: ["A. Dài hạn", "B. Ngắn hạn", "C. Vô hạn"], answer: "A", rationale: "" },
            { id: 129, question: "Công cụ nào sau đây là công cụ nợ?", options: ["A. Cổ phiếu thường", "B. Trái phiếu", "C. Cổ phiếu ưu đãi"], answer: "A", rationale: "" },
            { id: 130, question: "Công cụ nào sau đây là công cụ vốn?", options: ["A. Trái phiếu", "B. Cổ phiếu thường", "C. Hợp đồng tương lai"], answer: "A", rationale: "" },
            { id: 131, question: "Tín phiếu kho bạc được giao dịch trên thị trường:", options: ["A. Vốn", "B. Tiền tệ", "C. Chứng khoán"], answer: "B", rationale: "" },
            { id: 132, question: "Cổ phiếu được giao dịch trên thị trường:", options: ["A. Tiền tệ", "B. Vốn", "C. Tín dụng"], answer: "B", rationale: "" },
            { id: 133, question: "Ngân sách nhà nước là:", options: ["A. Tổng thu và chi của Nhà nước", "B. Các quỹ tiền tệ của Nhà nước", "C. Các khoản nợ của Nhà nước"], answer: "B", rationale: "" },
            { id: 134, question: "Thâm hụt ngân sách xảy ra khi:", options: ["A. Thu ngân sách lớn hơn chi ngân sách", "B. Chi ngân sách lớn hơn thu ngân sách", "C. Thu ngân sách bằng chi ngân sách"], answer: "B", rationale: "" },
            { id: 135, question: "Nguồn bù đắp thâm hụt ngân sách là:", options: ["A. Phát hành trái phiếu Chính phủ, vay nợ nước ngoài", "B. Tăng thuế, giảm chi tiêu", "C. Chỉ vay nợ từ Ngân hàng trung ương"], answer: "B", rationale: "" },
            { id: 136, question: "Tài chính doanh nghiệp có mục tiêu:", options: ["A. Tối đa hóa lợi nhuận", "B. Tối đa hóa doanh thu", "C. Tối đa hóa lợi ích của chủ sở hữu"], answer: "C", rationale: "" },
            { id: 137, question: "Quyết định đầu tư (Investment Decision) là:", options: ["A. Quyết định về cơ cấu vốn", "B. Quyết định về việc sử dụng vốn vào các tài sản và dự án", "C. Quyết định về chính sách cổ tức"], answer: "B", rationale: "" },
            { id: 138, question: "Quyết định tài trợ (Financing Decision) là:", options: ["A. Quyết định về việc sử dụng vốn vào các tài sản và dự án", "B. Quyết định về việc huy động vốn từ các nguồn khác nhau", "C. Quyết định về chính sách cổ tức"], answer: "B", rationale: "" },
            { id: 139, question: "Tái bảo hiểm là:", options: ["A. Bảo hiểm cho các cá nhân", "B. Bảo hiểm cho các doanh nghiệp", "C. Bảo hiểm cho các công ty bảo hiểm khác"], answer: "C", rationale: "" },
            { id: 140, question: "Cán cân thanh toán quốc tế là:", options: ["A. Bảng tổng hợp các giao dịch kinh tế giữa người cư trú và người không cư trú", "B. Báo cáo về tình hình nợ của một quốc gia", "C. Báo cáo về hoạt động xuất nhập khẩu"], answer: "B", rationale: "" },
            { id: 141, question: "Tài khoản vãng lai ghi nhận:", options: ["A. Chuyển giao vốn", "B. Hàng hóa, dịch vụ, thu nhập và chuyển giao vãng lai", "C. Đầu tư trực tiếp và gián tiếp"], answer: "B", rationale: "" },
            { id: 142, question: "Tài khoản tài chính ghi nhận:", options: ["A. Hàng hóa và dịch vụ", "B. Chuyển giao vốn", "C. Đầu tư trực tiếp, đầu tư gián tiếp và dự trữ ngoại hối"], answer: "B", rationale: "" },
            { id: 143, question: "FDI là:", options: ["A. Đầu tư nhằm thiết lập lợi ích lâu dài và ảnh hưởng đáng kể", "B. Mua cổ phiếu, trái phiếu với mục đích kiếm lợi nhuận ngắn hạn", "C. Các khoản cho vay của một quốc gia cho quốc gia khác"], answer: "B", rationale: "" },
            { id: 144, question: "Cơ chế tỷ giá hối đoái thả nổi là:", options: ["A. Tỷ giá được xác định bởi thị trường", "B. Tỷ giá được Ngân hàng trung ương ấn định", "C. Tỷ giá được xác định bởi tỷ lệ lạm phát"], answer: "B", rationale: "" },
            { id: 145, question: "Công cụ tài chính nào sau đây là công cụ phái sinh?", options: ["A. Cổ phiếu", "B. Hợp đồng tương lai", "C. Trái phiếu"], answer: "B", rationale: "" },
            { id: 146, question: "Trung gian tài chính có vai trò gì?", options: ["A. Chỉ nhận tiền gửi", "B. Chuyển vốn từ người dư thừa sang người thiếu hụt", "C. Chỉ cung cấp các khoản vay"], answer: "B", rationale: "" },
            { id: 147, question: "Rủi ro đạo đức (Moral Hazard) xảy ra:", options: ["A. Sau khi giao dịch diễn ra", "B. Trước khi giao dịch diễn ra", "C. Trong quá trình giao dịch"], answer: "B", rationale: "" },
            { id: 148, question: "Lựa chọn đối nghịch (Adverse Selection) xảy ra:", options: ["A. Sau khi giao dịch diễn ra", "B. Trước khi giao dịch diễn ra", "C. Trong quá trình giao dịch"], answer: "B", rationale: "" },
            { id: 149, question: "Công cụ nào được Ngân hàng trung ương sử dụng để điều tiết cung tiền?", options: ["A. Thuế", "B. Hoạt động thị trường mở", "C. Chi tiêu Chính phủ"], answer: "C", rationale: "" },
            { id: 150, question: "Chính sách tiền tệ mở rộng (nới lỏng) được thực hiện khi Ngân hàng trung ương:", options: ["A. Bán chứng khoán Chính phủ", "B. Mua chứng khoán Chính phủ", "C. Tăng lãi suất chiết khấu"], answer: "B", rationale: "" },
            { id: 151, question: "Chính sách tiền tệ thắt chặt được thực hiện khi Ngân hàng trung ương:", options: ["A. Bán chứng khoán Chính phủ", "B. Mua chứng khoán Chính phủ", "C. Giảm tỷ lệ dự trữ bắt buộc"], answer: "B", rationale: "" },
            { id: 152, question: "Trong phân phối lần đầu, thu nhập được phân phối cho những chủ thể nào?", options: ["A. Người lao động và người cho vay", "B. Người sở hữu các yếu tố sản xuất", "C. Người nhận trợ cấp xã hội"], answer: "A", rationale: "" },
            { id: 153, question: "Nguồn thu chính của Ngân sách Nhà nước là:", options: ["A. Các khoản viện trợ", "B. Thuế, phí, lệ phí", "C. Thu từ hoạt động kinh tế của Nhà nước"], answer: "A", rationale: "" },
            { id: 154, question: "Chi của Ngân sách Nhà nước bao gồm:", options: ["A. Chi đầu tư phát triển, chi thường xuyên, chi trả nợ", "B. Chỉ chi thường xuyên", "C. Chỉ chi trả nợ"], answer: "A", rationale: "" },
            { id: 155, question: "Nguồn vốn nào là vốn chủ sở hữu của doanh nghiệp?", options: ["A. Lợi nhuận giữ lại", "B. Vay ngân hàng", "C. Phát hành trái phiếu"], answer: "B", rationale: "" },
            { id: 156, question: "Nguồn vốn nào là vốn nợ của doanh nghiệp?", options: ["A. Cổ phiếu thường", "B. Vay ngân hàng", "C. Lợi nhuận giữ lại"], answer: "B", rationale: "" },
            { id: 157, question: "Mục tiêu của Quản trị vốn lưu động là:", options: ["A. Tối đa hóa lợi nhuận", "B. Đảm bảo khả năng thanh toán và hiệu quả sử dụng vốn", "C. Giảm thiểu chi phí"], answer: "B", rationale: "" },
            { id: 158, question: "Quyết định nào của tài chính doanh nghiệp liên quan đến cơ cấu vốn?", options: ["A. Quyết định đầu tư", "B. Quyết định tài trợ", "C. Quyết định chính sách cổ tức"], answer: "B", rationale: "" },
            { id: 159, question: "Công ty bảo hiểm sử dụng nguồn vốn nhàn rỗi chủ yếu để làm gì?", options: ["A. Chi trả bồi thường", "B. Đầu tư vào các tài sản tài chính", "C. Chi trả lương"], answer: "C", rationale: "" },
            { id: 160, question: "Trong cán cân thanh toán quốc tế, đầu tư trực tiếp nước ngoài (FDI) được ghi nhận ở:", options: ["A. Tài khoản vãng lai", "B. Tài khoản vốn", "C. Tài khoản tài chính"], answer: "B", rationale: "" },
            { id: 161, question: "Cơ chế tỷ giá hối đoái cố định có ưu điểm là:", options: ["A. Tăng tính ổn định và giảm rủi ro tỷ giá", "B. Tăng tính linh hoạt và khả năng điều chỉnh", "C. Giảm lạm phát"], answer: "A", rationale: "" },
            { id: 162, question: "Cơ chế tỷ giá hối đoái thả nổi có ưu điểm là:", options: ["A. Tăng tính ổn định và giảm rủi ro tỷ giá", "B. Tăng tính linh hoạt và khả năng điều chỉnh", "C. Giảm lạm phát"], answer: "B", rationale: "" },
            { id: 163, question: "Thị trường tài chính là:", options: ["A. Nơi giao dịch các công cụ tài chính", "B. Nơi giao dịch vốn trực tiếp giữa các chủ thể", "C. Nơi các chủ thể tìm kiếm và sử dụng vốn thông qua các khoản vay"], answer: "B", rationale: "" },
            { id: 164, question: "Vai trò của thị trường tài chính là:", options: ["A. Cung cấp vốn cho Nhà nước", "B. Phân bổ vốn hiệu quả và giảm thiểu rủi ro", "C. Kiểm soát các giao dịch của các công ty lớn"], answer: "B", rationale: "" },
            { id: 165, question: "Công cụ tài chính được chia thành:", options: ["A. Công cụ vốn và công cụ nợ", "B. Công cụ vốn, công cụ nợ và công cụ phái sinh", "C. Công cụ giao dịch và công cụ đầu tư"], answer: "B", rationale: "" },
            { id: 166, question: "Trung gian tài chính được phân loại thành:", options: ["A. Trung gian tiết kiệm và trung gian đầu tư", "B. Trung gian tiền gửi, trung gian tiết kiệm hợp đồng và trung gian đầu tư", "C. Trung gian ngân hàng và trung gian phi ngân hàng"], answer: "B", rationale: "" },
            { id: 167, question: "Ngân hàng trung ương có vai trò:", options: ["A. Quản lý các ngân hàng thương mại", "B. Quản lý chính sách tiền tệ, ổn định giá cả và tỷ giá hối đoái", "C. Cung cấp vốn cho các doanh nghiệp"], answer: "B", rationale: "" },
            { id: 168, question: "Hoạt động thị trường mở của Ngân hàng trung ương là:", options: ["A. Mua bán ngoại tệ", "B. Mua bán chứng khoán Chính phủ để điều tiết cung tiền", "C. Cho vay trực tiếp đối với các doanh nghiệp"], answer: "B", rationale: "" },
            { id: 169, question: "Chính sách tiền tệ mở rộng (nới lỏng) được thực hiện khi Ngân hàng trung ương:", options: ["A. Bán chứng khoán Chính phủ", "B. Mua chứng khoán Chính phủ", "C. Tăng lãi suất chiết khấu"], answer: "A", rationale: "" },
            { id: 170, question: "Chính sách tiền tệ thắt chặt được thực hiện khi Ngân hàng trung ương:", options: ["A. Bán chứng khoán Chính phủ", "B. Mua chứng khoán Chính phủ", "C. Giảm tỷ lệ dự trữ bắt buộc"], answer: "A", rationale: "" },
            { id: 171, question: "Tài chính công có vai trò:", options: ["A. Tạo lập và phân bổ các nguồn lực tài chính nhằm đáp ứng các nhu cầu của Nhà nước và toàn xã hội", "B. Chỉ tập trung vào việc thu thuế và chi tiêu Chính phủ", "C. Chỉ hỗ trợ các doanh nghiệp Nhà nước"], answer: "B", rationale: "" },
            { id: 172, question: "Nguồn thu của Ngân sách Nhà nước bao gồm:", options: ["A. Chỉ các khoản thuế", "B. Thuế, phí, lệ phí, thu từ hoạt động kinh tế của Nhà nước và các khoản viện trợ", "C. Chỉ các khoản vay từ Ngân hàng trung ương"], answer: "A", rationale: "" },
            { id: 173, question: "Thâm hụt ngân sách xảy ra khi:", options: ["A. Tổng thu ngân sách lớn hơn tổng chi ngân sách", "B. Tổng thu ngân sách nhỏ hơn tổng chi ngân sách", "C. Tổng thu ngân sách bằng tổng chi ngân sách"], answer: "A", rationale: "" },
            { id: 174, question: "Nguồn vốn nợ của doanh nghiệp là:", options: ["A. Cổ phiếu thường", "B. Vay ngân hàng", "C. Lợi nhuận giữ lại"], answer: "C", rationale: "" },
            { id: 175, question: "Mục tiêu của Quản trị vốn lưu động là:", options: ["A. Tối đa hóa lợi nhuận", "B. Đảm bảo khả năng thanh toán và hiệu quả sử dụng vốn", "C. Giảm thiểu chi phí"], answer: "C", rationale: "" },
            { id: 176, question: "Công ty bảo hiểm sử dụng Quỹ dự phòng nghiệp vụ bảo hiểm để làm gì?", options: ["A. Đầu tư vào các dự án rủi ro", "B. Chi trả bồi thường khi sự kiện bảo hiểm xảy ra", "C. Chi trả lương"], answer: "C", rationale: "" },
            { id: 177, question: "Cán cân thanh toán quốc tế bao gồm các tài khoản chính nào?", options: ["A. Chỉ tài khoản vãng lai", "B. Tài khoản vãng lai, tài khoản vốn và tài khoản tài chính", "C. Chỉ tài khoản vốn"], answer: "C", rationale: "" },
            { id: 178, question: "Tỷ giá hối đoái là:", options: ["A. Giá của một loại tiền tệ được biểu thị bằng vàng", "B. Giá của một đơn vị tiền tệ được biểu thị bằng một đơn vị tiền tệ khác", "C. Tỷ lệ lạm phát giữa hai quốc gia"], answer: "B", rationale: "" },
            { id: 179, question: "Cơ chế tỷ giá hối đoái thả nổi có ưu điểm là:", options: ["A. Tăng tính ổn định", "B. Tăng tính linh hoạt và khả năng điều chỉnh", "C. Giảm lạm phát"], answer: "A", rationale: "" },
            { id: 180, question: "Nguyên tắc quản lý tài chính công là:", options: ["A. Độc lập và tự chủ", "B. Công khai, minh bạch và hiệu quả", "C. Tập trung và thống nhất"], answer: "A", rationale: "" },
            { id: 181, question: "Thị trường sơ cấp là nơi:", options: ["A. Các công cụ tài chính được phát hành và bán lần đầu tiên", "B. Các công cụ tài chính được mua bán lại", "C. Các khoản vay được thực hiện"], answer: "A", rationale: "" },
            { id: 182, question: "Thị trường thứ cấp là nơi:", options: ["A. Các công cụ tài chính được phát hành và bán lần đầu tiên", "B. Các công cụ tài chính được mua bán lại", "C. Các khoản vay được thực hiện"], answer: "B", rationale: "" },
            { id: 183, question: "Vai trò của thị trường thứ cấp là:", options: ["A. Cung cấp vốn cho người phát hành", "B. Tăng tính thanh khoản cho các công cụ tài chính", "C. Giảm tính thanh khoản cho các công cụ tài chính"], answer: "B", rationale: "" },
            { id: 184, question: "Trung gian tiền gửi là:", options: ["A. Các công ty bảo hiểm", "B. Các ngân hàng thương mại", "C. Các quỹ tương hỗ"], answer: "B", rationale: "" },
            { id: 185, question: "Trung gian tiết kiệm hợp đồng là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ", "C. Các công ty bảo hiểm và các quỹ hưu trí"], answer: "B", rationale: "" },
            { id: 186, question: "Trung gian đầu tư là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ, các công ty đầu tư và các ngân hàng đầu tư", "C. Các công ty bảo hiểm"], answer: "B", rationale: "" },
            { id: 187, question: "Hoạt động thị trường mở mua chứng khoán Chính phủ sẽ:", options: ["A. Tăng cung tiền", "B. Giảm cung tiền", "C. Giữ nguyên cung tiền"], answer: "B", rationale: "" },
            { id: 188, question: "Hoạt động thị trường mở bán chứng khoán Chính phủ sẽ:", options: ["A. Tăng cung tiền", "B. Giảm cung tiền", "C. Giữ nguyên cung tiền"], answer: "B", rationale: "" },
            { id: 189, question: "Ngân sách Nhà nước có vai trò:", options: ["A. Điều tiết vĩ mô, ổn định kinh tế và tái phân phối thu nhập", "B. Chỉ tập trung vào chi tiêu quốc phòng", "C. Chỉ tập trung vào thu thuế"], answer: "C", rationale: "" },
            { id: 190, question: "Nguồn vốn nào là vốn chủ sở hữu của doanh nghiệp?", options: ["A. Vay ngân hàng", "B. Phát hành cổ phiếu", "C. Phát hành trái phiếu"], answer: "B", rationale: "" },
            { id: 191, question: "Nguồn vốn nào là vốn nợ của doanh nghiệp?", options: ["A. Phát hành cổ phiếu", "B. Vay ngân hàng", "C. Lợi nhuận giữ lại"], answer: "B", rationale: "" },
            { id: 192, question: "Mục tiêu của Tài chính doanh nghiệp là:", options: ["A. Tối đa hóa doanh thu", "B. Tối đa hóa lợi nhuận của chủ sở hữu", "C. Tối đa hóa sản lượng"], answer: "C", rationale: "" },
            { id: 193, question: "Cơ cấu vốn (Capital Structure) là:", options: ["A. Tỷ lệ giữa tài sản cố định và tài sản lưu động", "B. Tỷ lệ giữa các nguồn vốn dài hạn (vốn chủ sở hữu và nợ dài hạn)", "C. Tỷ lệ giữa các khoản thu và chi của doanh nghiệp"], answer: "B", rationale: "" },
            { id: 194, question: "Chính sách cổ tức (Dividend Policy) là:", options: ["A. Chính sách quyết định tỷ lệ nợ và vốn chủ sở hữu", "B. Chính sách quyết định tỷ lệ lợi nhuận được giữ lại tái đầu tư và lợi nhuận được chia cho cổ đông", "C. Chính sách quyết định mức lương cho nhân viên"], answer: "B", rationale: "" },
            { id: 195, question: "Hoạt động đầu tư của công ty bảo hiểm bao gồm:", options: ["A. Chỉ đầu tư vào các tài sản rủi ro", "B. Đầu tư vào các tài sản tài chính để sinh lời", "C. Chỉ đầu tư vào các tài sản ngắn hạn"], answer: "B", rationale: "" },
            { id: 196, question: "Tài khoản vãng lai thâm hụt khi:", options: ["A. Xuất khẩu lớn hơn nhập khẩu", "B. Xuất khẩu nhỏ hơn nhập khẩu", "C. Xuất khẩu bằng nhập khẩu"], answer: "C", rationale: "" },
            { id: 197, question: "Tài khoản vãng lai thâm hụt khi:", options: ["A. Xuất khẩu lớn hơn nhập khẩu", "B. Xuất khẩu nhỏ hơn nhập khẩu", "C. Xuất khẩu bằng nhập khẩu"], answer: "A", rationale: "" },
            { id: 198, question: "FPI là:", options: ["A. Đầu tư nhằm thiết lập lợi ích lâu dài", "B. Mua cổ phiếu, trái phiếu với mục đích kiếm lợi nhuận ngắn hạn", "C. Các khoản cho vay của một quốc gia cho quốc gia khác"], answer: "A", rationale: "" },
            { id: 199, question: "Cơ chế tỷ giá hối đoái cố định có nhược điểm là:", options: ["A. Giảm tính ổn định", "B. Giảm tính linh hoạt và khả năng điều chỉnh", "C. Tăng lạm phát"], answer: "A", rationale: "" },
            { id: 200, question: "Khái niệm tài chính là:", options: ["A. Tổng thể các quan hệ kinh tế phát sinh trong quá trình tạo lập và sử dụng các quỹ tiền tệ nhằm đáp ứng các mục tiêu khác nhau của các chủ thể trong xã hội", "B. Tiền tệ", "C. Sự dịch chuyển tiền tệ"], answer: "A", rationale: "" },
            { id: 201, question: "Tiền đề khách quan quyết định sự ra đời của tài chính là:", options: ["A. Sản xuất hàng hóa – tiền tệ và Nhà nước", "B. Chế độ công xã nguyên thủy", "C. Sự phân công lao động trong xã hội"], answer: "A", rationale: "" },
            { id: 202, question: "Phân phối lần đầu diễn ra trong lĩnh vực nào?", options: ["A. Lĩnh vực tài chính", "B. Lĩnh vực sản xuất và lưu thông hàng hóa", "C. Lĩnh vực tiêu dùng"], answer: "B", rationale: "" },
            { id: 203, question: "Phân phối lại là quá trình:", options: ["A. Phân phối lại thu nhập quốc dân cho các chủ thể kinh tế", "B. Phân phối thu nhập lần đầu", "C. Phân phối của cải vật chất"], answer: "B", rationale: "" },
            { id: 204, question: "Chức năng kiểm tra, giám sát tài chính là:", options: ["A. Việc giám sát quá trình sản xuất hàng hóa", "B. Việc giám sát toàn bộ quá trình tạo lập, phân bổ và sử dụng nguồn tài chính", "C. Việc kiểm tra các hoạt động kinh tế vĩ mô"], answer: "B", rationale: "" },
            { id: 205, question: "Hệ thống tài chính được hiểu là:", options: ["A. Tập hợp các ngân hàng và tổ chức tài chính", "B. Tập hợp các thị trường, các cá nhân và tổ chức giao dịch vốn với nhau, cùng với các quy định và giám sát hệ thống tài chính", "C. Tập hợp các cơ quan Chính phủ quản lý tài chính"], answer: "B", rationale: "" },
            { id: 206, question: "Thị trường tiền tệ là:", options: ["A. Thị trường giao dịch các công cụ có kỳ hạn ngắn (thường là dưới 1 năm)", "B. Thị trường giao dịch các công cụ có kỳ hạn dài", "C. Thị trường giao dịch các công cụ phái sinh"], answer: "B", rationale: "" },
            { id: 207, question: "Công cụ nào sau đây là công cụ nợ?", options: ["A. Trái phiếu", "B. Cổ phiếu thường", "C. Hợp đồng tương lai"], answer: "B", rationale: "" },
            { id: 208, question: "Tín phiếu kho bạc được giao dịch trên thị trường:", options: ["A. Vốn", "B. Tiền tệ", "C. Chứng khoán"], answer: "A", rationale: "" },
            { id: 209, question: "Cổ phiếu được giao dịch trên thị trường:", options: ["A. Tiền tệ", "B. Vốn", "C. Tín dụng"], answer: "B", rationale: "" },
            { id: 210, question: "Vai trò của thị trường thứ cấp là:", options: ["A. Cung cấp vốn cho người phát hành", "B. Tăng tính thanh khoản cho các công cụ tài chính", "C. Giảm tính thanh khoản cho các công cụ tài chính"], answer: "B", rationale: "" },
            { id: 211, question: "Trung gian tiền gửi là:", options: ["A. Các công ty bảo hiểm", "B. Các ngân hàng thương mại", "C. Các quỹ tương hỗ"], answer: "C", rationale: "" },
            { id: 212, question: "Trung gian tiết kiệm hợp đồng là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ", "C. Các công ty bảo hiểm và các quỹ hưu trí"], answer: "B", rationale: "" },
            { id: 213, question: "Rủi ro đạo đức (Moral Hazard) xảy ra:", options: ["A. Sau khi giao dịch diễn ra", "B. Trước khi giao dịch diễn ra", "C. Trong quá trình giao dịch"], answer: "A", rationale: "" },
            { id: 214, question: "Lựa chọn đối nghịch (Adverse Selection) xảy ra:", options: ["A. Sau khi giao dịch diễn ra", "B. Trước khi giao dịch diễn ra", "C. Trong quá trình giao dịch"], answer: "A", rationale: "" },
            { id: 215, question: "Công cụ nào được Ngân hàng trung ương sử dụng để điều tiết cung tiền?", options: ["A. Thuế", "B. Hoạt động thị trường mở, lãi suất chiết khấu và dự trữ bắt buộc", "C. Chi tiêu Chính phủ"], answer: "B", rationale: "" },
            { id: 216, question: "Chính sách tiền tệ mở rộng (nới lỏng) được thực hiện khi Ngân hàng trung ương:", options: ["A. Bán chứng khoán Chính phủ", "B. Mua chứng khoán Chính phủ", "C. Tăng lãi suất chiết khấu"], answer: "B", rationale: "" },
            { id: 217, question: "Nguồn thu chính của Ngân sách Nhà nước là:", options: ["A. Các khoản viện trợ", "B. Thuế, phí, lệ phí", "C. Thu từ hoạt động kinh tế của Nhà nước"], answer: "A", rationale: "" },
            { id: 218, question: "Nguồn vốn nợ của doanh nghiệp là:", options: ["A. Phát hành cổ phiếu", "B. Vay ngân hàng", "C. Lợi nhuận giữ lại"], answer: "A", rationale: "" },
            { id: 219, question: "Mục tiêu của Quản trị vốn lưu động là:", options: ["A. Tối đa hóa lợi nhuận", "B. Đảm bảo khả năng thanh toán và hiệu quả sử dụng vốn", "C. Giảm thiểu chi phí"], answer: "A", rationale: "" },
            { id: 220, question: "Công ty bảo hiểm sử dụng Quỹ dự phòng nghiệp vụ bảo hiểm để làm gì?", options: ["A. Đầu tư vào các dự án rủi ro", "B. Chi trả bồi thường khi sự kiện bảo hiểm xảy ra", "C. Chi trả lương"], answer: "C", rationale: "" },
            { id: 221, question: "Tài khoản vãng lai thâm hụt khi:", options: ["A. Xuất khẩu lớn hơn nhập khẩu", "B. Xuất khẩu nhỏ hơn nhập khẩu", "C. Xuất khẩu bằng nhập khẩu"], answer: "B", rationale: "" },
            { id: 222, question: "Cán cân thanh toán quốc tế bao gồm các tài khoản chính nào?", options: ["A. Tài khoản vãng lai, tài khoản vốn và tài khoản tài chính", "B. Chỉ tài khoản vãng lai", "C. Chỉ tài khoản vốn"], answer: "B", rationale: "" },
            { id: 223, question: "Tỷ giá hối đoái là:", options: ["A. Giá của một loại tiền tệ được biểu thị bằng vàng", "B. Giá của một đơn vị tiền tệ được biểu thị bằng một đơn vị tiền tệ khác", "C. Tỷ lệ lạm phát giữa hai quốc gia"], answer: "B", rationale: "" },
            { id: 224, question: "Cơ chế tỷ giá hối đoái cố định có ưu điểm là:", options: ["A. Tăng tính ổn định và giảm rủi ro tỷ giá", "B. Tăng tính linh hoạt và khả năng điều chỉnh", "C. Giảm lạm phát"], answer: "C", rationale: "" },
            { id: 225, question: "FDI là:", options: ["A. Đầu tư nhằm thiết lập lợi ích lâu dài và ảnh hưởng đáng kể", "B. Mua cổ phiếu, trái phiếu với mục đích kiếm lợi nhuận ngắn hạn", "C. Các khoản cho vay của một quốc gia cho quốc gia khác"], answer: "B", rationale: "" },
            { id: 226, question: "Tín dụng nhà nước là:", options: ["A. Các khoản cho vay của Nhà nước đối với các doanh nghiệp", "B. Các khoản vay của Nhà nước để bù đắp thâm hụt ngân sách", "C. Các khoản cho vay của Nhà nước đối với các cá nhân"], answer: "B", rationale: "" },
            { id: 227, question: "Nguyên tắc quản lý tài chính công là:", options: ["A. Độc lập và tự chủ", "B. Công khai, minh bạch và hiệu quả", "C. Tập trung và thống nhất"], answer: "B", rationale: "" },
            { id: 228, question: "Mục tiêu của Tài chính doanh nghiệp là:", options: ["A. Tối đa hóa doanh thu", "B. Tối đa hóa lợi nhuận của chủ sở hữu", "C. Tối đa hóa sản lượng"], answer: "A", rationale: "" },
            { id: 229, question: "Quản trị rủi ro tài chính (Financial Risk Management) là:", options: ["A. Quản lý các rủi ro liên quan đến hoạt động sản xuất", "B. Quản lý và giảm thiểu các rủi ro về lãi suất, tỷ giá, giá cả hàng hóa, và rủi ro tín dụng", "C. Quản lý các rủi ro về nhân sự"], answer: "A", rationale: "" },
            { id: 230, question: "Quỹ dự phòng nghiệp vụ bảo hiểm là:", options: ["A. Quỹ được sử dụng để đầu tư vào các dự án rủi ro", "B. Quỹ được hình thành từ phí bảo hiểm để chi trả bồi thường khi sự kiện bảo hiểm xảy ra", "C. Quỹ dùng để chi trả lương cho nhân viên"], answer: "B", rationale: "" },
            { id: 231, question: "Tài khoản vốn (Capital Account) ghi nhận các giao dịch về:", options: ["A. Hàng hóa và dịch vụ", "B. Chuyển giao vốn và mua bán tài sản phi tài chính, phi sản xuất", "C. Đầu tư trực tiếp và gián tiếp"], answer: "B", rationale: "" },
            { id: 232, question: "Hệ thống tiền tệ quốc tế (International Monetary System) là:", options: ["A. Tập hợp các quy tắc, công cụ và cơ chế điều chỉnh các giao dịch thanh toán quốc tế", "B. Tập hợp các ngân hàng trung ương trên thế giới", "C. Tập hợp các thị trường chứng khoán quốc tế"], answer: "A", rationale: "" },
            { id: 233, question: "Thị trường tiền tệ là nơi giao dịch các công cụ có kỳ hạn:", options: ["A. Dài hạn", "B. Ngắn hạn", "C. Vô hạn"], answer: "A", rationale: "" },
            { id: 234, question: "Thị trường vốn là nơi giao dịch các công cụ có kỳ hạn:", options: ["A. Dài hạn", "B. Ngắn hạn", "C. Vô hạn"], answer: "B", rationale: "" },
            { id: 235, question: "Công cụ nào sau đây là công cụ vốn?", options: ["A. Trái phiếu", "B. Cổ phiếu thường", "C. Hợp đồng tương lai"], answer: "C", rationale: "" },
            { id: 236, question: "Công cụ nào sau đây là công cụ phái sinh?", options: ["A. Cổ phiếu", "B. Hợp đồng tương lai", "C. Trái phiếu"], answer: "B", rationale: "" },
            { id: 237, question: "Trung gian đầu tư là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ, các công ty đầu tư và các ngân hàng đầu tư", "C. Các công ty bảo hiểm"], answer: "B", rationale: "" },
            { id: 238, question: "Hoạt động thị trường mở mua chứng khoán Chính phủ sẽ:", options: ["A. Tăng cung tiền", "B. Giảm cung tiền", "C. Giữ nguyên cung tiền"], answer: "C", rationale: "" },
            { id: 239, question: "Ngân sách Nhà nước có vai trò:", options: ["A. Điều tiết vĩ mô, ổn định kinh tế và tái phân phối thu nhập", "B. Chỉ tập trung vào chi tiêu quốc phòng", "C. Chỉ tập trung vào thu thuế"], answer: "A", rationale: "" },
            { id: 240, question: "Nguồn vốn nợ của doanh nghiệp là:", options: ["A. Phát hành cổ phiếu", "B. Vay ngân hàng", "C. Lợi nhuận giữ lại"], answer: "A", rationale: "" },
            { id: 241, question: "Hoạt động đầu tư của công ty bảo hiểm bao gồm:", options: ["A. Chỉ đầu tư vào các tài sản rủi ro", "B. Đầu tư vào các tài sản tài chính để sinh lời", "C. Chỉ đầu tư vào các tài sản ngắn hạn"], answer: "A", rationale: "" },
            { id: 242, question: "Tài khoản vãng lai thâm hụt khi:", options: ["A. Xuất khẩu lớn hơn nhập khẩu", "B. Xuất khẩu nhỏ hơn nhập khẩu", "C. Xuất khẩu bằng nhập khẩu"], answer: "A", rationale: "" },
            { id: 243, question: "Cơ chế tỷ giá hối đoái cố định có nhược điểm là:", options: ["A. Giảm tính ổn định", "B. Giảm tính linh hoạt và khả năng điều chỉnh", "C. Tăng lạm phát"], answer: "A", rationale: "" },
            { id: 244, question: "Thị trường sơ cấp là nơi:", options: ["A. Các công cụ tài chính được phát hành và bán lần đầu tiên", "B. Các công cụ tài chính được mua bán lại", "C. Các khoản vay được thực hiện"], answer: "B", rationale: "" },
            { id: 245, question: "Thị trường thứ cấp là nơi:", options: ["A. Các công cụ tài chính được phát hành và bán lần đầu tiên", "B. Các công cụ tài chính được mua bán lại", "C. Các khoản vay được thực hiện"], answer: "B", rationale: "" },
            { id: 246, question: "Vai trò của thị trường thứ cấp là:", options: ["A. Cung cấp vốn cho người phát hành", "B. Tăng tính thanh khoản cho các công cụ tài chính", "C. Giảm tính thanh khoản cho các công cụ tài chính"], answer: "C", rationale: "" },
            { id: 247, question: "Trung gian tiền gửi là:", options: ["A. Các công ty bảo hiểm", "B. Các ngân hàng thương mại", "C. Các quỹ tương hỗ"], answer: "A", rationale: "" },
            { id: 248, question: "Trung gian tiết kiệm hợp đồng là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ", "C. Các công ty bảo hiểm và các quỹ hưu trí"], answer: "A", rationale: "" },
            { id: 249, question: "Trung gian đầu tư là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ, các công ty đầu tư và các ngân hàng đầu tư", "C. Các công ty bảo hiểm"], answer: "B", rationale: "" },
            { id: 250, question: "Hoạt động thị trường mở bán chứng khoán Chính phủ sẽ:", options: ["A. Tăng cung tiền", "B. Giảm cung tiền", "C. Giữ nguyên cung tiền"], answer: "A", rationale: "" },
            { id: 251, question: "Chính sách tiền tệ thắt chặt được thực hiện khi Ngân hàng trung ương:", options: ["A. Bán chứng khoán Chính phủ", "B. Mua chứng khoán Chính phủ", "C. Giảm tỷ lệ dự trữ bắt buộc"], answer: "B", rationale: "" },
            { id: 252, question: "Nguồn thu chính của Ngân sách Nhà nước là:", options: ["A. Các khoản viện trợ", "B. Thuế, phí, lệ phí", "C. Thu từ hoạt động kinh tế của Nhà nước"], answer: "B", rationale: "" },
            { id: 253, question: "Chi của Ngân sách Nhà nước bao gồm:", options: ["A. Chi đầu tư phát triển, chi thường xuyên, chi trả nợ", "B. Chỉ chi thường xuyên", "C. Chỉ chi trả nợ"], answer: "C", rationale: "" },
            { id: 254, question: "Nguồn vốn nào là vốn chủ sở hữu của doanh nghiệp?", options: ["A. Lợi nhuận giữ lại", "B. Vay ngân hàng", "C. Phát hành trái phiếu"], answer: "B", rationale: "" },
            { id: 255, question: "Nguồn vốn nào là vốn nợ của doanh nghiệp?", options: ["A. Cổ phiếu thường", "B. Vay ngân hàng", "C. Lợi nhuận giữ lại"], answer: "A", rationale: "" },
            { id: 256, question: "Mục tiêu của Quản trị vốn lưu động là:", options: ["A. Tối đa hóa lợi nhuận", "B. Đảm bảo khả năng thanh toán và hiệu quả sử dụng vốn", "C. Giảm thiểu chi phí"], answer: "A", rationale: "" },
            { id: 257, question: "Quyết định nào của tài chính doanh nghiệp liên quan đến chính sách cổ tức?", options: ["A. Quyết định đầu tư", "B. Quyết định tài trợ", "C. Quyết định chính sách cổ tức"], answer: "B", rationale: "" },
            { id: 258, question: "Công ty bảo hiểm sử dụng nguồn vốn nhàn rỗi chủ yếu để làm gì?", options: ["A. Chi trả bồi thường", "B. Đầu tư vào các tài sản tài chính", "C. Chi trả lương"], answer: "C", rationale: "" },
            { id: 259, question: "Trong cán cân thanh toán quốc tế, đầu tư gián tiếp nước ngoài (FPI) được ghi nhận ở:", options: ["A. Tài khoản vãng lai", "B. Tài khoản vốn", "C. Tài khoản tài chính"], answer: "B", rationale: "" },
            { id: 260, question: "Cơ chế tỷ giá hối đoái thả nổi có ưu điểm là:", options: ["A. Tăng tính ổn định", "B. Tăng tính linh hoạt và khả năng điều chỉnh", "C. Giảm lạm phát"], answer: "A", rationale: "" },
            { id: 261, question: "Công cụ tài chính nào sau đây là công cụ phái sinh?", options: ["A. Cổ phiếu", "B. Hợp đồng tương lai", "C. Trái phiếu"], answer: "A", rationale: "" },
            { id: 262, question: "Rủi ro đạo đức (Moral Hazard) xảy ra:", options: ["A. Sau khi giao dịch diễn ra", "B. Trước khi giao dịch diễn ra", "C. Trong quá trình giao dịch"], answer: "A", rationale: "" },
            { id: 263, question: "Nguồn bù đắp thâm hụt ngân sách là:", options: ["A. Phát hành trái phiếu Chính phủ, vay nợ nước ngoài", "B. Tăng thuế, giảm chi tiêu", "C. Chỉ vay nợ từ Ngân hàng trung ương"], answer: "B", rationale: "" },
            { id: 264, question: "Tài chính công có vai trò:", options: ["A. Tạo lập và phân bổ các nguồn lực tài chính nhằm đáp ứng các nhu cầu của Nhà nước và toàn xã hội", "B. Chỉ tập trung vào việc thu thuế và chi tiêu Chính phủ", "C. Chỉ hỗ trợ các doanh nghiệp Nhà nước"], answer: "A", rationale: "" },
            { id: 265, question: "Thâm hụt ngân sách xảy ra khi:", options: ["A. Tổng thu ngân sách lớn hơn tổng chi ngân sách", "B. Tổng thu ngân sách nhỏ hơn tổng chi ngân sách", "C. Tổng thu ngân sách bằng tổng chi ngân sách"], answer: "A", rationale: "" },
            { id: 266, question: "Hoạt động huy động vốn của doanh nghiệp bao gồm:", options: ["A. Chỉ huy động vốn từ ngân hàng", "B. Huy động vốn từ bên trong và bên ngoài", "C. Chỉ huy động vốn từ các cổ đông sáng lập"], answer: "B", rationale: "" },
            { id: 267, question: "Hoạt động đầu tư của doanh nghiệp bao gồm:", options: ["A. Đầu tư vào tài sản cố định, tài sản lưu động và các dự án", "B. Chỉ đầu tư vào các tài sản ngắn hạn", "C. Chỉ đầu tư vào các tài sản dài hạn"], answer: "C", rationale: "" },
            { id: 268, question: "Tái bảo hiểm là:", options: ["A. Bảo hiểm cho các cá nhân", "B. Bảo hiểm cho các doanh nghiệp", "C. Bảo hiểm cho các công ty bảo hiểm khác"], answer: "B", rationale: "" },
            { id: 269, question: "Tài khoản vãng lai thâm hụt khi:", options: ["A. Xuất khẩu lớn hơn nhập khẩu", "B. Xuất khẩu nhỏ hơn nhập khẩu", "C. Xuất khẩu bằng nhập khẩu"], answer: "A", rationale: "" },
            { id: 270, question: "Cán cân thanh toán quốc tế là:", options: ["A. Bảng tổng hợp các giao dịch kinh tế giữa người cư trú và người không cư trú", "B. Báo cáo về tình hình nợ của một quốc gia", "C. Báo cáo về hoạt động xuất nhập khẩu"], answer: "A", rationale: "" },
            { id: 271, question: "Tỷ giá hối đoái là:", options: ["A. Giá của một loại tiền tệ được biểu thị bằng vàng", "B. Giá của một đơn vị tiền tệ được biểu thị bằng một đơn vị tiền tệ khác", "C. Tỷ lệ lạm phát giữa hai quốc gia"], answer: "A", rationale: "" },
            { id: 272, question: "Cơ chế tỷ giá hối đoái cố định có nhược điểm là:", options: ["A. Giảm tính ổn định", "B. Giảm tính linh hoạt và khả năng điều chỉnh", "C. Tăng lạm phát"], answer: "A", rationale: "" },
            { id: 273, question: "Khái niệm tài chính là:", options: ["A. Tổng thể các quan hệ kinh tế phát sinh trong quá trình tạo lập và sử dụng các quỹ tiền tệ nhằm đáp ứng các mục tiêu khác nhau của các chủ thể trong xã hội", "B. Tiền tệ", "C. Sự dịch chuyển tiền tệ"], answer: "A", rationale: "" },
            { id: 274, question: "Tiền đề khách quan quyết định sự ra đời của tài chính là:", options: ["A. Sản xuất hàng hóa – tiền tệ và Nhà nước", "B. Chế độ công xã nguyên thủy", "C. Sự phân công lao động trong xã hội"], answer: "B", rationale: "" },
            { id: 275, question: "Phân phối lần đầu diễn ra trong lĩnh vực nào?", options: ["A. Lĩnh vực tài chính", "B. Lĩnh vực sản xuất và lưu thông hàng hóa", "C. Lĩnh vực tiêu dùng"], answer: "B", rationale: "" },
            { id: 276, question: "Chức năng kiểm tra, giám sát tài chính là:", options: ["A. Việc giám sát quá trình sản xuất hàng hóa", "B. Việc giám sát toàn bộ quá trình tạo lập, phân bổ và sử dụng nguồn tài chính", "C. Việc kiểm tra các hoạt động kinh tế vĩ mô"], answer: "B", rationale: "" },
            { id: 277, question: "Hệ thống tài chính được hiểu là:", options: ["A. Tập hợp các ngân hàng và tổ chức tài chính", "B. Tập hợp các thị trường, các cá nhân và tổ chức giao dịch vốn với nhau, cùng với các quy định và giám sát hệ thống tài chính", "C. Tập hợp các cơ quan Chính phủ quản lý tài chính"], answer: "C", rationale: "" },
            { id: 278, question: "Thị trường tiền tệ là:", options: ["A. Thị trường giao dịch các công cụ có kỳ hạn ngắn (thường là dưới 1 năm)", "B. Thị trường giao dịch các công cụ có kỳ hạn dài", "C. Thị trường giao dịch các công cụ phái sinh"], answer: "A", rationale: "" },
            { id: 279, question: "Công cụ nào sau đây là công cụ nợ?", options: ["A. Trái phiếu", "B. Cổ phiếu thường", "C. Hợp đồng tương lai"], answer: "A", rationale: "" },
            { id: 280, question: "Cổ phiếu được giao dịch trên thị trường:", options: ["A. Tiền tệ", "B. Vốn", "C. Tín dụng"], answer: "A", rationale: "" },
            { id: 281, question: "Vai trò của thị trường thứ cấp là:", options: ["A. Cung cấp vốn cho người phát hành", "B. Tăng tính thanh khoản cho các công cụ tài chính", "C. Giảm tính thanh khoản cho các công cụ tài chính"], answer: "B", rationale: "" },
            { id: 282, question: "Trung gian tiền gửi là:", options: ["A. Các công ty bảo hiểm", "B. Các ngân hàng thương mại", "C. Các quỹ tương hỗ"], answer: "B", rationale: "" },
            { id: 283, question: "Trung gian tiết kiệm hợp đồng là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ", "C. Các công ty bảo hiểm và các quỹ hưu trí"], answer: "B", rationale: "" },
            { id: 284, question: "Rủi ro đạo đức (Moral Hazard) xảy ra:", options: ["A. Sau khi giao dịch diễn ra", "B. Trước khi giao dịch diễn ra", "C. Trong quá trình giao dịch"], answer: "B", rationale: "" },
            { id: 285, question: "Lựa chọn đối nghịch (Adverse Selection) xảy ra:", options: ["A. Sau khi giao dịch diễn ra", "B. Trước khi giao dịch diễn ra", "C. Trong quá trình giao dịch"], answer: "B", rationale: "" },
            { id: 286, question: "Công cụ nào được Ngân hàng trung ương sử dụng để điều tiết cung tiền?", options: ["A. Thuế", "B. Hoạt động thị trường mở, lãi suất chiết khấu và dự trữ bắt buộc", "C. Chi tiêu Chính phủ"], answer: "B", rationale: "" },
            { id: 287, question: "Chính sách tiền tệ mở rộng (nới lỏng) được thực hiện khi Ngân hàng trung ương:", options: ["A. Bán chứng khoán Chính phủ", "B. Mua chứng khoán Chính phủ", "C. Tăng lãi suất chiết khấu"], answer: "B", rationale: "" },
            { id: 288, question: "Nguồn thu chính của Ngân sách Nhà nước là:", options: ["A. Các khoản viện trợ", "B. Thuế, phí, lệ phí", "C. Thu từ hoạt động kinh tế của Nhà nước"], answer: "A", rationale: "" },
            { id: 289, question: "Nguồn vốn nợ của doanh nghiệp là:", options: ["A. Phát hành cổ phiếu", "B. Vay ngân hàng", "C. Lợi nhuận giữ lại"], answer: "A", rationale: "" },
            { id: 290, question: "Mục tiêu của Quản trị vốn lưu động là:", options: ["A. Tối đa hóa lợi nhuận", "B. Đảm bảo khả năng thanh toán và hiệu quả sử dụng vốn", "C. Giảm thiểu chi phí"], answer: "A", rationale: "" },
            { id: 291, question: "Công ty bảo hiểm sử dụng Quỹ dự phòng nghiệp vụ bảo hiểm để làm gì?", options: ["A. Đầu tư vào các dự án rủi ro", "B. Chi trả bồi thường khi sự kiện bảo hiểm xảy ra", "C. Chi trả lương"], answer: "A", rationale: "" },
            { id: 292, question: "Tài khoản vốn (Capital Account) ghi nhận các giao dịch về:", options: ["A. Hàng hóa và dịch vụ", "B. Chuyển giao vốn và mua bán tài sản phi tài chính, phi sản xuất", "C. Đầu tư trực tiếp và gián tiếp"], answer: "A", rationale: "" },
            { id: 293, question: "Hệ thống tiền tệ quốc tế (International Monetary System) là:", options: ["A. Tập hợp các quy tắc, công cụ và cơ chế điều chỉnh các giao dịch thanh toán quốc tế", "B. Tập hợp các ngân hàng trung ương trên thế giới", "C. Tập hợp các thị trường chứng khoán quốc tế"], answer: "C", rationale: "" },
            { id: 294, question: "Thị trường tiền tệ là nơi giao dịch các công cụ có kỳ hạn:", options: ["A. Dài hạn", "B. Ngắn hạn", "C. Vô hạn"], answer: "B", rationale: "" },
            { id: 295, question: "Thị trường vốn là nơi giao dịch các công cụ có kỳ hạn:", options: ["A. Dài hạn", "B. Ngắn hạn", "C. Vô hạn"], answer: "B", rationale: "" },
            { id: 296, question: "Công cụ nào sau đây là công cụ vốn?", options: ["A. Trái phiếu", "B. Cổ phiếu thường", "C. Hợp đồng tương lai"], answer: "B", rationale: "" },
            { id: 297, question: "Công cụ nào sau đây là công cụ phái sinh?", options: ["A. Cổ phiếu", "B. Hợp đồng tương lai", "C. Trái phiếu"], answer: "B", rationale: "" },
            { id: 298, question: "Trung gian đầu tư là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ, các công ty đầu tư và các ngân hàng đầu tư", "C. Các công ty bảo hiểm"], answer: "C", rationale: "" },
            { id: 299, question: "Hoạt động thị trường mở mua chứng khoán Chính phủ sẽ:", options: ["A. Tăng cung tiền", "B. Giảm cung tiền", "C. Giữ nguyên cung tiền"], answer: "B", rationale: "" },
            { id: 300, question: "Ngân sách Nhà nước có vai trò:", options: ["A. Điều tiết vĩ mô, ổn định kinh tế và tái phân phối thu nhập", "B. Chỉ tập trung vào chi tiêu quốc phòng", "C. Chỉ tập trung vào thu thuế"], answer: "A", rationale: "" },
            { id: 301, question: "Nguồn vốn nợ của doanh nghiệp là:", options: ["A. Phát hành cổ phiếu", "B. Vay ngân hàng", "C. Lợi nhuận giữ lại"], answer: "B", rationale: "" },
            { id: 302, question: "Hoạt động đầu tư của công ty bảo hiểm bao gồm:", options: ["A. Chỉ đầu tư vào các tài sản rủi ro", "B. Đầu tư vào các tài sản tài chính để sinh lời", "C. Chỉ đầu tư vào các tài sản ngắn hạn"], answer: "B", rationale: "" },
            { id: 303, question: "Tài khoản vãng lai thâm hụt khi:", options: ["A. Xuất khẩu lớn hơn nhập khẩu", "B. Xuất khẩu nhỏ hơn nhập khẩu", "C. Xuất khẩu bằng nhập khẩu"], answer: "C", rationale: "" },
            { id: 304, question: "Cơ chế tỷ giá hối đoái cố định có nhược điểm là:", options: ["A. Giảm tính ổn định", "B. Giảm tính linh hoạt và khả năng điều chỉnh", "C. Tăng lạm phát"], answer: "B", rationale: "" },
            { id: 305, question: "Thị trường sơ cấp là nơi:", options: ["A. Các công cụ tài chính được phát hành và bán lần đầu tiên", "B. Các công cụ tài chính được mua bán lại", "C. Các khoản vay được thực hiện"], answer: "A", rationale: "" },
            { id: 306, question: "Thị trường thứ cấp là nơi:", options: ["A. Các công cụ tài chính được phát hành và bán lần đầu tiên", "B. Các công cụ tài chính được mua bán lại", "C. Các khoản vay được thực hiện"], answer: "A", rationale: "" },
            { id: 307, question: "Vai trò của thị trường thứ cấp là:", options: ["A. Cung cấp vốn cho người phát hành", "B. Tăng tính thanh khoản cho các công cụ tài chính", "C. Giảm tính thanh khoản cho các công cụ tài chính"], answer: "B", rationale: "" },
            { id: 308, question: "Trung gian tiền gửi là:", options: ["A. Các công ty bảo hiểm", "B. Các ngân hàng thương mại", "C. Các quỹ tương hỗ"], answer: "C", rationale: "" },
            { id: 309, question: "Trung gian tiết kiệm hợp đồng là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ", "C. Các công ty bảo hiểm và các quỹ hưu trí"], answer: "B", rationale: "" },
            { id: 310, question: "Trung gian đầu tư là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ, các công ty đầu tư và các ngân hàng đầu tư", "C. Các công ty bảo hiểm"], answer: "B", rationale: "" },
            { id: 311, question: "Hoạt động thị trường mở bán chứng khoán Chính phủ sẽ:", options: ["A. Tăng cung tiền", "B. Giảm cung tiền", "C. Giữ nguyên cung tiền"], answer: "B", rationale: "" },
            { id: 312, question: "Chính sách tiền tệ thắt chặt được thực hiện khi Ngân hàng trung ương:", options: ["A. Bán chứng khoán Chính phủ", "B. Mua chứng khoán Chính phủ", "C. Giảm tỷ lệ dự trữ bắt buộc"], answer: "B", rationale: "" },
            { id: 313, question: "Nguồn thu chính của Ngân sách Nhà nước là:", options: ["A. Các khoản viện trợ", "B. Thuế, phí, lệ phí", "C. Thu từ hoạt động kinh tế của Nhà nước"], answer: "B", rationale: "" },
            { id: 314, question: "Chi của Ngân sách Nhà nước bao gồm:", options: ["A. Chi đầu tư phát triển, chi thường xuyên, chi trả nợ", "B. Chỉ chi thường xuyên", "C. Chỉ chi trả nợ"], answer: "A", rationale: "" },
            { id: 315, question: "Nguồn vốn nào là vốn chủ sở hữu của doanh nghiệp?", options: ["A. Lợi nhuận giữ lại", "B. Vay ngân hàng", "C. Phát hành trái phiếu"], answer: "A", rationale: "" },
            { id: 316, question: "Nguồn vốn nào là vốn nợ của doanh nghiệp?", options: ["A. Cổ phiếu thường", "B. Vay ngân hàng", "C. Lợi nhuận giữ lại"], answer: "A", rationale: "" },
            { id: 317, question: "Mục tiêu của Quản trị vốn lưu động là:", options: ["A. Tối đa hóa lợi nhuận", "B. Đảm bảo khả năng thanh toán và hiệu quả sử dụng vốn", "C. Giảm thiểu chi phí"], answer: "A", rationale: "" },
            { id: 318, question: "Quyết định nào của tài chính doanh nghiệp liên quan đến chính sách cổ tức?", options: ["A. Quyết định đầu tư", "B. Quyết định tài trợ", "C. Quyết định chính sách cổ tức"], answer: "A", rationale: "" },
            { id: 319, question: "Công ty bảo hiểm sử dụng nguồn vốn nhàn rỗi chủ yếu để làm gì?", options: ["A. Chi trả bồi thường", "B. Đầu tư vào các tài sản tài chính", "C. Chi trả lương"], answer: "B", rationale: "" },
            { id: 320, question: "Trong cán cân thanh toán quốc tế, đầu tư gián tiếp nước ngoài (FPI) được ghi nhận ở:", options: ["A. Tài khoản vãng lai", "B. Tài khoản vốn", "C. Tài khoản tài chính"], answer: "B", rationale: "" },
            { id: 321, question: "Cơ chế tỷ giá hối đoái thả nổi có ưu điểm là:", options: ["A. Tăng tính ổn định", "B. Tăng tính linh hoạt và khả năng điều chỉnh", "C. Giảm lạm phát"], answer: "B", rationale: "" },
            { id: 322, question: "Công cụ tài chính nào sau đây là công cụ phái sinh?", options: ["A. Cổ phiếu", "B. Hợp đồng tương lai", "C. Trái phiếu"], answer: "B", rationale: "" },
            { id: 323, question: "Rủi ro đạo đức (Moral Hazard) xảy ra:", options: ["A. Sau khi giao dịch diễn ra", "B. Trước khi giao dịch diễn ra", "C. Trong quá trình giao dịch"], answer: "B", rationale: "" },
            { id: 324, question: "Nguồn bù đắp thâm hụt ngân sách là:", options: ["A. Phát hành trái phiếu Chính phủ, vay nợ nước ngoài", "B. Tăng thuế, giảm chi tiêu", "C. Chỉ vay nợ từ Ngân hàng trung ương"], answer: "A", rationale: "" },
            { id: 325, question: "Tài chính công có vai trò:", options: ["A. Tạo lập và phân bổ các nguồn lực tài chính nhằm đáp ứng các nhu cầu của Nhà nước và toàn xã hội", "B. Chỉ tập trung vào việc thu thuế và chi tiêu Chính phủ", "C. Chỉ hỗ trợ các doanh nghiệp Nhà nước"], answer: "A", rationale: "" },
            { id: 326, question: "Thâm hụt ngân sách xảy ra khi:", options: ["A. Tổng thu ngân sách lớn hơn tổng chi ngân sách", "B. Tổng thu ngân sách nhỏ hơn tổng chi ngân sách", "C. Tổng thu ngân sách bằng tổng chi ngân sách"], answer: "A", rationale: "" },
            { id: 327, question: "Hoạt động huy động vốn của doanh nghiệp bao gồm:", options: ["A. Chỉ huy động vốn từ ngân hàng", "B. Huy động vốn từ bên trong và bên ngoài", "C. Chỉ huy động vốn từ các cổ đông sáng lập"], answer: "B", rationale: "" },
            { id: 328, question: "Hoạt động đầu tư của doanh nghiệp bao gồm:", options: ["A. Đầu tư vào tài sản cố định, tài sản lưu động và các dự án", "B. Chỉ đầu tư vào các tài sản ngắn hạn", "C. Chỉ đầu tư vào các tài sản dài hạn"], answer: "A", rationale: "" },
            { id: 329, question: "Tái bảo hiểm là:", options: ["A. Bảo hiểm cho các cá nhân", "B. Bảo hiểm cho các doanh nghiệp", "C. Bảo hiểm cho các công ty bảo hiểm khác"], answer: "B", rationale: "" },
            { id: 330, question: "Tài khoản vãng lai thâm hụt khi:", options: ["A. Xuất khẩu lớn hơn nhập khẩu", "B. Xuất khẩu nhỏ hơn nhập khẩu", "C. Xuất khẩu bằng nhập khẩu"], answer: "B", rationale: "" },
            { id: 331, question: "Cán cân thanh toán quốc tế là:", options: ["A. Bảng tổng hợp các giao dịch kinh tế giữa người cư trú và người không cư trú", "B. Báo cáo về tình hình nợ của một quốc gia", "C. Báo cáo về hoạt động xuất nhập khẩu"], answer: "C", rationale: "" },
            { id: 332, question: "Tỷ giá hối đoái là:", options: ["A. Giá của một loại tiền tệ được biểu thị bằng vàng", "B. Giá của một đơn vị tiền tệ được biểu thị bằng một đơn vị tiền tệ khác", "C. Tỷ lệ lạm phát giữa hai quốc gia"], answer: "B", rationale: "" },
            { id: 333, question: "Cơ chế tỷ giá hối đoái cố định có nhược điểm là:", options: ["A. Giảm tính ổn định", "B. Giảm tính linh hoạt và khả năng điều chỉnh", "C. Tăng lạm phát"], answer: "B", rationale: "" },
            { id: 334, question: "Khái niệm tài chính là:", options: ["A. Tổng thể các quan hệ kinh tế phát sinh trong quá trình tạo lập và sử dụng các quỹ tiền tệ nhằm đáp ứng các mục tiêu khác nhau của các chủ thể trong xã hội", "B. Tiền tệ", "C. Sự dịch chuyển tiền tệ"], answer: "B", rationale: "" },
            { id: 335, question: "Tiền đề khách quan quyết định sự ra đời của tài chính là:", options: ["A. Sản xuất hàng hóa – tiền tệ và Nhà nước", "B. Chế độ công xã nguyên thủy", "C. Sự phân công lao động trong xã hội"], answer: "B", rationale: "" },
            { id: 336, question: "Phân phối lần đầu diễn ra trong lĩnh vực nào?", options: ["A. Lĩnh vực tài chính", "B. Lĩnh vực sản xuất và lưu thông hàng hóa", "C. Lĩnh vực tiêu dùng"], answer: "B", rationale: "" },
            { id: 337, question: "Chức năng kiểm tra, giám sát tài chính là:", options: ["A. Việc giám sát quá trình sản xuất hàng hóa", "B. Việc giám sát toàn bộ quá trình tạo lập, phân bổ và sử dụng nguồn tài chính", "C. Việc kiểm tra các hoạt động kinh tế vĩ mô"], answer: "B", rationale: "" },
            { id: 338, question: "Hệ thống tài chính được hiểu là:", options: ["A. Tập hợp các ngân hàng và tổ chức tài chính", "B. Tập hợp các thị trường, các cá nhân và tổ chức giao dịch vốn với nhau, cùng với các quy định và giám sát hệ thống tài chính", "C. Tập hợp các cơ quan Chính phủ quản lý tài chính"], answer: "B", rationale: "" },
            { id: 339, question: "Thị trường tiền tệ là:", options: ["A. Thị trường giao dịch các công cụ có kỳ hạn ngắn (thường là dưới 1 năm)", "B. Thị trường giao dịch các công cụ có kỳ hạn dài", "C. Thị trường giao dịch các công cụ phái sinh"], answer: "A", rationale: "" },
            { id: 340, question: "Công cụ nào sau đây là công cụ nợ?", options: ["A. Trái phiếu", "B. Cổ phiếu thường", "C. Hợp đồng tương lai"], answer: "B", rationale: "" },
            { id: 341, question: "Cổ phiếu được giao dịch trên thị trường:", options: ["A. Tiền tệ", "B. Vốn", "C. Tín dụng"], answer: "B", rationale: "" },
            { id: 342, question: "Vai trò của thị trường thứ cấp là:", options: ["A. Cung cấp vốn cho người phát hành", "B. Tăng tính thanh khoản cho các công cụ tài chính", "C. Giảm tính thanh khoản cho các công cụ tài chính"], answer: "B", rationale: "" },
            { id: 343, question: "Trung gian tiền gửi là:", options: ["A. Các công ty bảo hiểm", "B. Các ngân hàng thương mại", "C. Các quỹ tương hỗ"], answer: "A", rationale: "" },
            { id: 344, question: "Trung gian tiết kiệm hợp đồng là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ", "C. Các công ty bảo hiểm và các quỹ hưu trí"], answer: "C", rationale: "" },
            { id: 345, question: "Rủi ro đạo đức (Moral Hazard) xảy ra:", options: ["A. Sau khi giao dịch diễn ra", "B. Trước khi giao dịch diễn ra", "C. Trong quá trình giao dịch"], answer: "A", rationale: "" },
            { id: 346, question: "Lựa chọn đối nghịch (Adverse Selection) xảy ra:", options: ["A. Sau khi giao dịch diễn ra", "B. Trước khi giao dịch diễn ra", "C. Trong quá trình giao dịch"], answer: "A", rationale: "" },
            { id: 347, question: "Công cụ nào được Ngân hàng trung ương sử dụng để điều tiết cung tiền?", options: ["A. Thuế", "B. Hoạt động thị trường mở, lãi suất chiết khấu và dự trữ bắt buộc", "C. Chi tiêu Chính phủ"], answer: "B", rationale: "" },
            { id: 348, question: "Chính sách tiền tệ mở rộng (nới lỏng) được thực hiện khi Ngân hàng trung ương:", options: ["A. Bán chứng khoán Chính phủ", "B. Mua chứng khoán Chính phủ", "C. Tăng lãi suất chiết khấu"], answer: "A", rationale: "" },
            { id: 349, question: "Nguồn thu chính của Ngân sách Nhà nước là:", options: ["A. Các khoản viện trợ", "B. Thuế, phí, lệ phí", "C. Thu từ hoạt động kinh tế của Nhà nước"], answer: "B", rationale: "" },
            { id: 350, question: "Nguồn vốn nợ của doanh nghiệp là:", options: ["A. Phát hành cổ phiếu", "B. Vay ngân hàng", "C. Lợi nhuận giữ lại"], answer: "B", rationale: "" },
            { id: 351, question: "Mục tiêu của Quản trị vốn lưu động là:", options: ["A. Tối đa hóa lợi nhuận", "B. Đảm bảo khả năng thanh toán và hiệu quả sử dụng vốn", "C. Giảm thiểu chi phí"], answer: "B", rationale: "" },
            { id: 352, question: "Công ty bảo hiểm sử dụng Quỹ dự phòng nghiệp vụ bảo hiểm để làm gì?", options: ["A. Đầu tư vào các dự án rủi ro", "B. Chi trả bồi thường khi sự kiện bảo hiểm xảy ra", "C. Chi trả lương"], answer: "A", rationale: "" },
            { id: 353, question: "Tài khoản vốn (Capital Account) ghi nhận các giao dịch về:", options: ["A. Hàng hóa và dịch vụ", "B. Chuyển giao vốn và mua bán tài sản phi tài chính, phi sản xuất", "C. Đầu tư trực tiếp và gián tiếp"], answer: "B", rationale: "" },
            { id: 354, question: "Hệ thống tiền tệ quốc tế (International Monetary System) là:", options: ["A. Tập hợp các quy tắc, công cụ và cơ chế điều chỉnh các giao dịch thanh toán quốc tế", "B. Tập hợp các ngân hàng trung ương trên thế giới", "C. Tập hợp các thị trường chứng khoán quốc tế"], answer: "A", rationale: "" },
            { id: 355, question: "Thị trường tiền tệ là nơi giao dịch các công cụ có kỳ hạn:", options: ["A. Dài hạn", "B. Ngắn hạn", "C. Vô hạn"], answer: "A", rationale: "" },
            { id: 356, question: "Thị trường vốn là nơi giao dịch các công cụ có kỳ hạn:", options: ["A. Dài hạn", "B. Ngắn hạn", "C. Vô hạn"], answer: "B", rationale: "" },
            { id: 357, question: "Công cụ nào sau đây là công cụ vốn?", options: ["A. Trái phiếu", "B. Cổ phiếu thường", "C. Hợp đồng tương lai"], answer: "B", rationale: "" },
            { id: 358, question: "Công cụ nào sau đây là công cụ phái sinh?", options: ["A. Cổ phiếu", "B. Hợp đồng tương lai", "C. Trái phiếu"], answer: "B", rationale: "" },
            { id: 359, question: "Trung gian đầu tư là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ, các công ty đầu tư và các ngân hàng đầu tư", "C. Các công ty bảo hiểm"], answer: "A", rationale: "" },
            { id: 360, question: "Hoạt động thị trường mở mua chứng khoán Chính phủ sẽ:", options: ["A. Tăng cung tiền", "B. Giảm cung tiền", "C. Giữ nguyên cung tiền"], answer: "B", rationale: "" },
            { id: 361, question: "Ngân sách Nhà nước có vai trò:", options: ["A. Điều tiết vĩ mô, ổn định kinh tế và tái phân phối thu nhập", "B. Chỉ tập trung vào chi tiêu quốc phòng", "C. Chỉ tập trung vào thu thuế"], answer: "B", rationale: "" },
            { id: 362, question: "Nguồn vốn nợ của doanh nghiệp là:", options: ["A. Phát hành cổ phiếu", "B. Vay ngân hàng", "C. Lợi nhuận giữ lại"], answer: "B", rationale: "" },
            { id: 363, question: "Hoạt động đầu tư của công ty bảo hiểm bao gồm:", options: ["A. Chỉ đầu tư vào các tài sản rủi ro", "B. Đầu tư vào các tài sản tài chính để sinh lời", "C. Chỉ đầu tư vào các tài sản ngắn hạn"], answer: "B", rationale: "" },
            { id: 364, question: "Tài khoản vãng lai thâm hụt khi:", options: ["A. Xuất khẩu lớn hơn nhập khẩu", "B. Xuất khẩu nhỏ hơn nhập khẩu", "C. Xuất khẩu bằng nhập khẩu"], answer: "B", rationale: "" },
            { id: 365, question: "Cơ chế tỷ giá hối đoái cố định có nhược điểm là:", options: ["A. Giảm tính ổn định", "B. Giảm tính linh hoạt và khả năng điều chỉnh", "C. Tăng lạm phát"], answer: "A", rationale: "" },
            { id: 366, question: "Thị trường sơ cấp là nơi:", options: ["A. Các công cụ tài chính được phát hành và bán lần đầu tiên", "B. Các công cụ tài chính được mua bán lại", "C. Các khoản vay được thực hiện"], answer: "A", rationale: "" },
            { id: 367, question: "Thị trường thứ cấp là nơi:", options: ["A. Các công cụ tài chính được phát hành và bán lần đầu tiên", "B. Các công cụ tài chính được mua bán lại", "C. Các khoản vay được thực hiện"], answer: "C", rationale: "" },
            { id: 368, question: "Vai trò của thị trường thứ cấp là:", options: ["A. Cung cấp vốn cho người phát hành", "B. Tăng tính thanh khoản cho các công cụ tài chính", "C. Giảm tính thanh khoản cho các công cụ tài chính"], answer: "B", rationale: "" },
            { id: 369, question: "Trung gian tiền gửi là:", options: ["A. Các công ty bảo hiểm", "B. Các ngân hàng thương mại", "C. Các quỹ tương hỗ"], answer: "C", rationale: "" },
            { id: 370, question: "Trung gian tiết kiệm hợp đồng là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ", "C. Các công ty bảo hiểm và các quỹ hưu trí"], answer: "C", rationale: "" },
            { id: 371, question: "Trung gian đầu tư là:", options: ["A. Các ngân hàng thương mại", "B. Các quỹ tương hỗ, các công ty đầu tư và các ngân hàng đầu tư", "C. Các công ty bảo hiểm"], answer: "C", rationale: "" },
            { id: 372, question: "Hoạt động thị trường mở bán chứng khoán Chính phủ sẽ:", options: ["A. Tăng cung tiền", "B. Giảm cung tiền", "C. Giữ nguyên cung tiền"], answer: "C", rationale: "" },
            { id: 373, question: "Chính sách tiền tệ thắt chặt được thực hiện khi Ngân hàng trung ương:", options: ["A. Bán chứng khoán Chính phủ", "B. Mua chứng khoán Chính phủ", "C. Giảm tỷ lệ dự trữ bắt buộc"], answer: "A", rationale: "" },
            { id: 374, question: "Nguồn thu chính của Ngân sách Nhà nước là:", options: ["A. Các khoản viện trợ", "B. Thuế, phí, lệ phí", "C. Thu từ hoạt động kinh tế của Nhà nước"], answer: "B", rationale: "" },
            { id: 375, question: "Chi của Ngân sách Nhà nước bao gồm:", options: ["A. Chi đầu tư phát triển, chi thường xuyên, chi trả nợ", "B. Chỉ chi thường xuyên", "C. Chỉ chi trả nợ"], answer: "B", rationale: "" },
            { id: 376, question: "Nguồn vốn nào là vốn chủ sở hữu của doanh nghiệp?", options: ["A. Lợi nhuận giữ lại", "B. Vay ngân hàng", "C. Phát hành trái phiếu"], answer: "B", rationale: "" },
            { id: 377, question: "Nguồn vốn nào là vốn nợ của doanh nghiệp?", options: ["A. Cổ phiếu thường", "B. Vay ngân hàng", "C. Lợi nhuận giữ lại"], answer: "A", rationale: "" },
            { id: 378, question: "Mục tiêu của Quản trị vốn lưu động là:", options: ["A. Tối đa hóa lợi nhuận", "B. Đảm bảo khả năng thanh toán và hiệu quả sử dụng vốn", "C. Giảm thiểu chi phí"], answer: "B", rationale: "" },
            { id: 379, question: "Quyết định nào của tài chính doanh nghiệp liên quan đến chính sách cổ tức?", options: ["A. Quyết định đầu tư", "B. Quyết định tài trợ", "C. Quyết định chính sách cổ tức"], answer: "B", rationale: "" },
            { id: 380, question: "Công ty bảo hiểm sử dụng nguồn vốn nhàn rỗi chủ yếu để làm gì?", options: ["A. Chi trả bồi thường", "B. Đầu tư vào các tài sản tài chính", "C. Chi trả lương"], answer: "A", rationale: "" },
            { id: 381, question: "Trong cán cân thanh toán quốc tế, đầu tư gián tiếp nước ngoài (FPI) được ghi nhận ở:", options: ["A. Tài khoản vãng lai", "B. Tài khoản vốn", "C. Tài khoản tài chính"], answer: "B", rationale: "" },
            { id: 382, question: "Cơ chế tỷ giá hối đoái thả nổi có ưu điểm là:", options: ["A. Tăng tính ổn định", "B. Tăng tính linh hoạt và khả năng điều chỉnh", "C. Giảm lạm phát"], answer: "B", rationale: "" },
            { id: 383, question: "Công cụ tài chính nào sau đây là công cụ phái sinh?", options: ["A. Cổ phiếu", "B. Hợp đồng tương lai", "C. Trái phiếu"], answer: "A", rationale: "" },
            { id: 384, question: "Rủi ro đạo đức (Moral Hazard) xảy ra:", options: ["A. Sau khi giao dịch diễn ra", "B. Trước khi giao dịch diễn ra", "C. Trong quá trình giao dịch"], answer: "B", rationale: "" },
            { id: 385, question: "Nguồn bù đắp thâm hụt ngân sách là:", options: ["A. Phát hành trái phiếu Chính phủ, vay nợ nước ngoài", "B. Tăng thuế, giảm chi tiêu", "C. Chỉ vay nợ từ Ngân hàng trung ương"], answer: "B", rationale: "" },
            { id: 386, question: "Tài chính công có vai trò:", options: ["A. Tạo lập và phân bổ các nguồn lực tài chính nhằm đáp ứng các nhu cầu của Nhà nước và toàn xã hội", "B. Chỉ tập trung vào việc thu thuế và chi tiêu Chính phủ", "C. Chỉ hỗ trợ các doanh nghiệp Nhà nước"], answer: "B", rationale: "" },
            { id: 387, question: "Thâm hụt ngân sách xảy ra khi:", options: ["A. Tổng thu ngân sách lớn hơn tổng chi ngân sách", "B. Tổng thu ngân sách nhỏ hơn tổng chi ngân sách", "C. Tổng thu ngân sách bằng tổng chi ngân sách"], answer: "B", rationale: "" },
            { id: 388, question: "Hoạt động huy động vốn của doanh nghiệp bao gồm:", options: ["A. Chỉ huy động vốn từ ngân hàng", "B. Huy động vốn từ bên trong và bên ngoài", "C. Chỉ huy động vốn từ các cổ đông sáng lập"], answer: "A", rationale: "" },
            { id: 389, question: "Hoạt động đầu tư của doanh nghiệp bao gồm:", options: ["A. Đầu tư vào tài sản cố định, tài sản lưu động và các dự án", "B. Chỉ đầu tư vào các tài sản ngắn hạn", "C. Chỉ đầu tư vào các tài sản dài hạn"], answer: "B", rationale: "" },
            { id: 390, question: "Tái bảo hiểm là:", options: ["A. Bảo hiểm cho các cá nhân", "B. Bảo hiểm cho các doanh nghiệp", "C. Bảo hiểm cho các công ty bảo hiểm khác"], answer: "A", rationale: "" },
            { id: 391, question: "Tài khoản vãng lai thâm hụt khi:", options: ["A. Xuất khẩu lớn hơn nhập khẩu", "B. Xuất khẩu nhỏ hơn nhập khẩu", "C. Xuất khẩu bằng nhập khẩu"], answer: "C", rationale: "" },
            { id: 392, question: "Cán cân thanh toán quốc tế là:", options: ["A. Bảng tổng hợp các giao dịch kinh tế giữa người cư trú và người không cư trú", "B. Báo cáo về tình hình nợ của một quốc gia", "C. Báo cáo về hoạt động xuất nhập khẩu"], answer: "B", rationale: "" },
            { id: 393, question: "Tỷ giá hối đoái là:", options: ["A. Giá của một loại tiền tệ được biểu thị bằng vàng", "B. Giá của một đơn vị tiền tệ được biểu thị bằng một đơn vị tiền tệ khác", "C. Tỷ lệ lạm phát giữa hai quốc gia"], answer: "B", rationale: "" },
            { id: 394, question: "Cơ chế tỷ giá hối đoái cố định có nhược điểm là:", options: ["A. Giảm tính ổn định", "B. Giảm tính linh hoạt và khả năng điều chỉnh", "C. Tăng lạm phát"], answer: "B", rationale: "" },
            { id: 395, question: "Khái niệm tài chính là:", options: ["A. Tổng thể các quan hệ kinh tế phát sinh trong quá trình tạo lập và sử dụng các quỹ tiền tệ nhằm đáp ứng các mục tiêu khác nhau của các chủ thể trong xã hội", "B. Tiền tệ", "C. Sự dịch chuyển tiền tệ"], answer: "B", rationale: "" },
            { id: 396, question: "Tiền đề khách quan quyết định sự ra đời của tài chính là:", options: ["A. Sản xuất hàng hóa – tiền tệ và Nhà nước", "B. Chế độ công xã nguyên thủy", "C. Sự phân công lao động trong xã hội"], answer: "B", rationale: "" },
            { id: 397, question: "Phân phối lần đầu diễn ra trong lĩnh vực nào?", options: ["A. Lĩnh vực tài chính", "B. Lĩnh vực sản xuất và lưu thông hàng hóa", "C. Lĩnh vực tiêu dùng"], answer: "B", rationale: "" },
            { id: 398, question: "Chức năng kiểm tra, giám sát tài chính là:", options: ["A. Việc giám sát quá trình sản xuất hàng hóa", "B. Việc giám sát toàn bộ quá trình tạo lập, phân bổ và sử dụng nguồn tài chính", "C. Việc kiểm tra các hoạt động kinh tế vĩ mô"], answer: "A", rationale: "" },
            { id: 399, question: "Hệ thống tài chính được hiểu là:", options: ["A. Tập hợp các ngân hàng và tổ chức tài chính", "B. Tập hợp các thị trường, các cá nhân và tổ chức giao dịch vốn với nhau, cùng với các quy định và giám sát hệ thống tài chính", "C. Tập hợp các cơ quan Chính phủ quản lý tài chính"], answer: "C", rationale: "" },
            { id: 400, question: "Thị trường tiền tệ là:", options: ["A. Thị trường giao dịch các công cụ có kỳ hạn ngắn (thường là dưới 1 năm)", "B. Thị trường giao dịch các công cụ có kỳ hạn dài", "C. Thị trường giao dịch các công cụ phái sinh"], answer: "A", rationale: "" },
            { id: 401, question: "Một nhà đầu tư quốc tế muốn tìm kiếm cơ hội đầu tư tại quốc gia có lợi thế về thuế thấp và quy định lỏng lẻo. Mục tiêu của họ chủ yếu là:", options: ["A. Tăng trưởng doanh thu ngắn hạn.", "B. Tránh thuế và tối ưu hóa lợi nhuận.", "C. Mở rộng thị trường tiêu thụ sản phẩm."], answer: "B", rationale: "" },
            { id: 402, question: "Đầu tư gián tiếp nước ngoài chủ yếu được thực hiện qua hình thức nào?", options: ["A. Mua cổ phần của doanh nghiệp quốc gia khác.", "B. Đầu tư vào các quỹ đầu tư quốc tế và trái phiếu quốc tế.", "C. Đầu tư trực tiếp vào các doanh nghiệp quốc gia khác"], answer: "B", rationale: "" },
            { id: 403, question: "Một công ty Nhật Bản quyết định đầu tư vào một nhà máy sản xuất ô tô tại Việt Nam, nắm giữ 100% cổ phần của nhà máy này. Công ty Nhật Bản cung cấp toàn bộ vốn đầu tư và điều hành hoạt động sản xuất tại Việt Nam. Đây là ví dụ về hình thức tài chính quốc tế nào?", options: ["A. Đầu tư gián tiếp nước ngoài", "B. Đầu tư trực tiếp nước ngoài", "C. Viện trợ phát triển chính thức ODA"], answer: "B", rationale: "" },
            { id: 404, question: "FDI có thể dẫn đến sự 'chuyển giao công nghệ' trong quốc gia nhận đầu tư. Điều này có nghĩa là gì?", options: ["A. Các công ty quốc tế chỉ cung cấp vốn đầu tư mà không chia sẻ bất kỳ công nghệ nào", "B. Công nghệ, kỹ năng quản lý và bí quyết được chuyển từ công ty mẹ sang công ty con, giúp quốc gia nhận đầu tư nâng cao năng suất", "C. Quốc gia nhận đầu tư phải mua toàn bộ công nghệ từ công ty mẹ"], answer: "B", rationale: "" }
        ];

        // --- QUIZ LOGIC (Giữ nguyên từ code gốc) ---
        let currentQuestionIndex = 0;
        let score = 0;
        let answeredQuestions = [];
        let isAnswered = false;

        // Load answered state from localStorage if available (cho phiên ôn tập không liên quan đến Firebase)
        function loadState() {
            const savedState = localStorage.getItem('quiz_404_state');
            if (savedState) {
                const state = JSON.parse(savedState);
                currentQuestionIndex = state.currentQuestionIndex;
                score = state.score;
                answeredQuestions = state.answeredQuestions;
                
                // Merge user answers back into quizData
                state.quizDataWithAnswers.forEach(qA => {
                    const qD = quizData.find(q => q.id === qA.id);
                    if (qD) {
                        qD.userAnswer = qA.userAnswer;
                    }
                });
            }
        }

        // Save current state to localStorage
        function saveState() {
            const state = {
                currentQuestionIndex,
                score,
                answeredQuestions,
                quizDataWithAnswers: quizData.map(q => ({ id: q.id, userAnswer: q.userAnswer }))
            };
            localStorage.setItem('quiz_404_state', JSON.stringify(state));
        }

        function renderQuiz() {
            const quizArea = document.getElementById('quiz-area');
            quizArea.innerHTML = ''; // Clear previous content

            if (currentQuestionIndex >= quizData.length) {
                renderResults(quizArea);
                return;
            }

            const currentQ = quizData[currentQuestionIndex];
            isAnswered = currentQ.userAnswer !== undefined;

            const optionsHtml = currentQ.options.map((option, index) => {
                const optionLetter = String.fromCharCode(65 + index);
                let classes = 'option-button w-full p-4 mt-3 rounded-xl shadow hover:shadow-lg transition-all duration-200 ';
                let clickHandler = `selectOption(${currentQ.id}, '${optionLetter}')`;
                
                // If answered, set correct/incorrect classes
                if (isAnswered) {
                    const userSelection = currentQ.userAnswer;
                    if (optionLetter === currentQ.answer) {
                        classes += 'bg-green-100 text-green-700 font-bold border-2 border-green-500';
                    } else if (optionLetter === userSelection && optionLetter !== currentQ.answer) {
                        classes += 'bg-red-100 text-red-700 font-bold border-2 border-red-500';
                    } else {
                        classes += 'bg-gray-50 text-gray-800 border border-gray-200';
                    }
                    clickHandler = ''; // Disable clicking after answering
                } else {
                    classes += 'bg-gray-50 text-gray-800 border border-gray-200 hover:bg-gray-100';
                }

                return `<button onclick="${clickHandler}" class="${classes}">${option}</button>`;
            }).join('');

            const rationaleHtml = currentQ.rationale && isAnswered ? 
                `<div class="mt-6 p-4 bg-yellow-50 border-l-4 border-yellow-500 rounded-lg">
                    <h4 class="font-bold text-yellow-700">Giải thích:</h4>
                    <p class="text-gray-700 mt-2">${currentQ.rationale}</p>
                </div>` : '';

            const questionHtml = `
                <div class="mb-6 border-b pb-4">
                    <p class="text-xl font-bold text-custom-blue">Câu Hỏi ${currentQuestionIndex + 1} / ${quizData.length}</p>
                </div>
                <div class="question-wrapper">
                    <p class="text-2xl font-semibold text-gray-800 mb-6">${currentQ.id}. ${currentQ.question}</p>
                    <div id="options-area" class="flex flex-col">
                        ${optionsHtml}
                    </div>
                    ${rationaleHtml}
                </div>
                <div class="flex justify-between items-center pt-6 border-t mt-6">
                    <button onclick="navigateQuestion(-1)" ${currentQuestionIndex === 0 ? 'disabled' : ''} class="px-4 py-2 bg-gray-300 text-gray-800 rounded-xl hover:bg-gray-400 disabled:bg-gray-200 transition-all duration-200">
                        <i class="fas fa-chevron-left mr-2"></i> Câu trước
                    </button>
                    <p class="text-lg font-medium text-gray-600">Trạng thái: <span class="text-custom-blue font-semibold">${answeredQuestions.length}/${quizData.length}</span></p>
                    <button onclick="navigateQuestion(1)" id="next-button" class="px-4 py-2 bg-custom-blue text-white rounded-xl hover:bg-blue-700 transition-all duration-200">
                        ${currentQuestionIndex === quizData.length - 1 ? 'Xem kết quả' : 'Câu tiếp theo'} <i class="fas fa-chevron-right ml-2"></i>
                    </button>
                </div>
            `;
            quizArea.innerHTML = questionHtml;
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function selectOption(qId, selectedLetter) {
            const currentQ = quizData.find(q => q.id === qId);
            if (currentQ.userAnswer !== undefined) return;

            currentQ.userAnswer = selectedLetter;
            if (!answeredQuestions.includes(qId)) {
                answeredQuestions.push(qId);
            }
            
            if (selectedLetter === currentQ.answer) {
                score++;
            }

            saveState(); // Save state immediately after answering
            updateScore();
            
            // Re-render the current question to show correct/incorrect status and rationale
            renderQuiz();
        }
        
        // Recalculate score and answeredQuestions count
        function updateScore() {
            score = 0;
            answeredQuestions = [];
            quizData.forEach(q => {
                if (q.userAnswer !== undefined) {
                    answeredQuestions.push(q.id);
                    if (q.userAnswer === q.answer) {
                        score++;
                    }
                }
            });
        }


        function navigateQuestion(direction) {
            if (direction === 1 && currentQuestionIndex < quizData.length - 1) {
                currentQuestionIndex++;
            } else if (direction === -1 && currentQuestionIndex > 0) {
                currentQuestionIndex--;
            } else if (direction === 1 && currentQuestionIndex === quizData.length - 1) {
                renderResults(document.getElementById('quiz-area'));
                return;
            }
            saveState(); // Save state when navigating
            renderQuiz();
        }

        function renderResults(quizArea) {
            updateScore(); // Ensure final score is accurate
            const percentage = (score / quizData.length) * 100;
            const resultClass = percentage >= 80 ? 'text-green-600' : (percentage >= 50 ? 'text-yellow-600' : 'text-red-600');

            const reviewHtml = quizData.map(q => {
                const isCorrect = q.userAnswer === q.answer;
                const icon = isCorrect ? '<i class="fas fa-check-circle text-green-500"></i>' : '<i class="fas fa-times-circle text-red-500"></i>';
                const answerClass = isCorrect ? 'text-green-600' : 'text-red-600';
                const userChoice = q.options.find(opt => opt.startsWith(q.userAnswer)) || 'Chưa trả lời';
                
                return `
                    <div class="mb-6 p-4 border border-gray-200 rounded-lg shadow-sm">
                        <div class="flex items-start mb-2">
                            <div class="mr-3 mt-1">${icon}</div>
                            <p class="font-semibold text-gray-800">${q.id}. ${q.question}</p>
                        </div>
                        <p class="ml-7 text-sm ${q.userAnswer ? answerClass : 'text-gray-500'}">Lựa chọn của bạn: <b>${userChoice.substring(0, 1)}</b>. ${userChoice.substring(3)}</p>
                        <p class="ml-7 text-sm text-green-600 font-bold">Đáp án đúng: <b>${q.options.find(opt => opt.startsWith(q.answer)).substring(0, 1)}</b>. ${q.options.find(opt => opt.startsWith(q.answer)).substring(3)}</p>
                    </div>
                `;
            }).join('');

            quizArea.innerHTML = `
                <h2 class="text-4xl font-bold text-center mb-4 text-custom-blue">KẾT QUẢ BÀI TẬP</h2>
                <div class="text-center mb-8">
                    <p class="text-2xl font-semibold text-gray-700">Số câu đúng: <span class="font-extrabold ${resultClass}">${score}/${quizData.length}</span></p>
                    <p class="text-4xl font-extrabold mt-2 ${resultClass}">${percentage.toFixed(2)}%</p>
                </div>
                
                <div class="flex justify-center mb-8">
                    <button id="toggle-review-button" onclick="toggleReview()" class="px-6 py-3 bg-gray-500 hover:bg-gray-600 text-white font-semibold rounded-xl shadow transition-all duration-300">
                        <i class="fas fa-eye mr-2"></i> Xem lại các câu hỏi
                    </button>
                </div>

                <div id="review-area" class="mt-8 pt-4 border-t border-gray-300 hidden">
                    <h3 class="text-2xl font-bold text-gray-800 mb-4">Phần Xem Lại Chi Tiết</h3>
                    ${reviewHtml}
                </div>
            `;
            document.getElementById('reset-button').classList.remove('hidden');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function toggleReview() {
            const reviewArea = document.getElementById('review-area');
            const button = document.getElementById('toggle-review-button');
            if (reviewArea.classList.contains('hidden')) {
                reviewArea.classList.remove('hidden');
                button.innerHTML = '<i class="fas fa-eye-slash mr-2"></i> Ẩn phần xem lại';
            } else {
                reviewArea.classList.add('hidden');
                button.innerHTML = '<i class="fas fa-eye mr-2"></i> Xem lại các câu hỏi';
            }
        }

        function resetQuiz() {
            if (!window.confirm("Bạn có chắc chắn muốn làm lại bài kiểm tra? Tất cả kết quả hiện tại sẽ bị xóa.")) {
                 return; 
            }
            currentQuestionIndex = 0;
            score = 0;
            answeredQuestions = [];
            isAnswered = false;
            // Reset user answers in data
            quizData.forEach(q => delete q.userAnswer);
            localStorage.removeItem('quiz_404_state');
            document.getElementById('reset-button').classList.add('hidden');
            renderQuiz();
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Initialize quiz on window load
        window.onload = function() {
            // Check for a simpler, non-alert confirmation method
            window.confirm = (message) => {
                const quizArea = document.getElementById('quiz-area');
                const modalHtml = `
                    <div id="custom-confirm-modal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
                        <div class="bg-white p-8 rounded-lg shadow-2xl max-w-sm w-full">
                            <p class="text-lg font-semibold mb-6">${message}</p>
                            <div class="flex justify-end space-x-4">
                                <button id="confirm-cancel" class="px-4 py-2 bg-gray-300 text-gray-800 rounded-lg hover:bg-gray-400 transition">Hủy</button>
                                <button id="confirm-ok" class="px-4 py-2 bg-red-600 text-white rounded-lg hover:bg-red-700 transition">Đồng ý</button>
                            </div>
                        </div>
                    </div>
                `;
                quizArea.insertAdjacentHTML('afterend', modalHtml);

                return new Promise(resolve => {
                    const modal = document.getElementById('custom-confirm-modal');
                    document.getElementById('confirm-ok').onclick = () => {
                        modal.remove();
                        resolve(true);
                    };
                    document.getElementById('confirm-cancel').onclick = () => {
                        modal.remove();
                        resolve(false);
                    };
                });
            };
            
            loadState();
            updateScore(); // Recalculate score from loaded data
            renderQuiz();
        };
    </script>
</body>
</html>
