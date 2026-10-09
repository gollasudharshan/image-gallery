<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">

    <!-- Makes the website responsive on mobile devices -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>My Image Gallery</title>

    <style>

        /* ==============================
           BASIC RESET
        ============================== */

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }


        /* ==============================
           BODY
        ============================== */

        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #667eea, #764ba2);
            min-height: 100vh;
            padding: 30px 15px;
        }


        /* ==============================
           MAIN CONTAINER
        ============================== */

        .container {
            max-width: 1200px;
            margin: auto;
            background: white;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.25);
        }


        /* ==============================
           PAGE TITLE
        ============================== */

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 25px;
            font-size: 36px;
        }


        /* ==============================
           FILTER BUTTONS
        ============================== */

        .filters {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 30px;
        }

        .filter-btn {
            border: none;
            padding: 12px 22px;
            border-radius: 25px;
            background: #eeeeee;
            color: #333;
            cursor: pointer;
            font-size: 15px;
            transition: 0.3s;
        }

        .filter-btn:hover {
            background: #667eea;
            color: white;
            transform: translateY(-2px);
        }

        .filter-btn.active {
            background: #667eea;
            color: white;
        }


        /* ==============================
           IMAGE GALLERY
        ============================== */

        .gallery {
            display: grid;

            /* Responsive columns */
            grid-template-columns: repeat(
                auto-fit,
                minmax(250px, 1fr)
            );

            gap: 20px;
        }


        /* ==============================
           GALLERY IMAGE CARD
        ============================== */

        .gallery-item {
            position: relative;
            overflow: hidden;
            border-radius: 15px;
            cursor: pointer;
            height: 230px;
            background: #ddd;
            transition: 0.3s;
        }

        .gallery-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.25);
        }


        /* ==============================
           IMAGES
        ============================== */

        .gallery-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;

            /* Smooth zoom effect */
            transition: transform 0.5s ease;
        }

        .gallery-item:hover img {
            transform: scale(1.1);
        }


        /* ==============================
           IMAGE TITLE
        ============================== */

        .image-title {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;

            padding: 15px;

            color: white;
            font-size: 18px;
            font-weight: bold;

            background: linear-gradient(
                transparent,
                rgba(0, 0, 0, 0.8)
            );

            transform: translateY(100%);
            transition: 0.4s;
        }

        .gallery-item:hover .image-title {
            transform: translateY(0);
        }


        /* ==============================
           LIGHTBOX
        ============================== */

        .lightbox {
            display: none;

            position: fixed;
            z-index: 1000;

            top: 0;
            left: 0;

            width: 100%;
            height: 100%;

            background: rgba(0, 0, 0, 0.9);

            justify-content: center;
            align-items: center;
        }

        .lightbox.active {
            display: flex;
        }


        /* ==============================
           LIGHTBOX IMAGE
        ============================== */

        .lightbox img {
            max-width: 80%;
            max-height: 80%;

            border-radius: 10px;

            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.5);

            animation: zoomIn 0.3s ease;
        }


        /* Lightbox animation */

        @keyframes zoomIn {

            from {
                transform: scale(0.7);
                opacity: 0;
            }

            to {
                transform: scale(1);
                opacity: 1;
            }

        }


        /* ==============================
           CLOSE BUTTON
        ============================== */

        .close-btn {
            position: absolute;

            top: 25px;
            right: 35px;

            font-size: 40px;
            color: white;

            cursor: pointer;

            transition: 0.3s;
        }

        .close-btn:hover {
            color: #667eea;
            transform: rotate(90deg);
        }


        /* ==============================
           PREVIOUS / NEXT BUTTONS
        ============================== */

        .nav-btn {
            position: absolute;

            top: 50%;

            transform: translateY(-50%);

            border: none;

            width: 55px;
            height: 55px;

            border-radius: 50%;

            background: rgba(255, 255, 255, 0.2);

            color: white;

            font-size: 30px;

            cursor: pointer;

            transition: 0.3s;
        }

        .nav-btn:hover {
            background: #667eea;
        }

        .prev {
            left: 30px;
        }

        .next {
            right: 30px;
        }


        /* ==============================
           RESPONSIVE DESIGN
        ============================== */

        @media (max-width: 600px) {

            body {
                padding: 15px;
            }

            .container {
                padding: 20px;
            }

            h1 {
                font-size: 28px;
            }

            .gallery {
                grid-template-columns: 1fr;
            }

            .gallery-item {
                height: 250px;
            }

            .lightbox img {
                max-width: 90%;
                max-height: 70%;
            }

            .nav-btn {
                width: 45px;
                height: 45px;
                font-size: 22px;
            }

            .prev {
                left: 10px;
            }

            .next {
                right: 10px;
            }

        }

    </style>

</head>


<body>


    <!-- ==============================
         MAIN CONTAINER
    ============================== -->

    <div class="container">

        <h1>📸 My Image Gallery</h1>


        <!-- ==============================
             FILTER BUTTONS
        ============================== -->

        <div class="filters">

            <button
                class="filter-btn active"
                data-filter="all">
                All
            </button>

            <button
                class="filter-btn"
                data-filter="nature">
                Nature
            </button>

            <button
                class="filter-btn"
                data-filter="city">
                City
            </button>

            <button
                class="filter-btn"
                data-filter="animals">
                Animals
            </button>

        </div>


        <!-- ==============================
             IMAGE GALLERY
        ============================== -->

        <div class="gallery">


            <!-- Nature Image 1 -->

            <div
                class="gallery-item"
                data-category="nature"
                data-index="0">

                <img
                    src="C:\Users\balak\OneDrive\Desktop\istockphoto-638943746-170667a.jpg"
                    alt="Nature">

                <div class="image-title">
                    Beautiful Nature
                </div>

            </div>


            <!-- Nature Image 2 -->

            <div
                class="gallery-item"
                data-category="nature"
                data-index="1">

                <img
                    src="C:\Users\balak\OneDrive\Desktop\images.jpg"
                    alt="Mountain">

                <div class="image-title">
                    Mountain View
                </div>

            </div>


            <!-- City Image 1 -->

            <div
                class="gallery-item"
                data-category="city"
                data-index="2">

                <img
                    src="C:\Users\balak\OneDrive\Desktop\images (1).jpg"
                    alt="City">

                <div class="image-title">
                    Beautiful City
                </div>

            </div>


            <!-- City Image 2 -->

            <div
                class="gallery-item"
                data-category="city"
                data-index="3">

                <img
                    src="C:\Users\balak\OneDrive\Desktop\images (2).jpg"
                    alt="City Night">

                <div class="image-title">
                    City at Night
                </div>

            </div>


            <!-- Animal Image 1 -->

            <div
                class="gallery-item"
                data-category="animals"
                data-index="4">

                <img
                    src="C:\Users\balak\OneDrive\Desktop\images (3).jpg"
                    alt="Animal">

                <div class="image-title">
                    Cute Animal
                </div>

            </div>


            <!-- Animal Image 2 -->

            <div
                class="gallery-item"
                data-category="animals"
                data-index="5">

                <img
                    src="C:\Users\balak\OneDrive\Desktop\Fierce-Felines-of-the-Jungle-Exploring-the-World-of-Wild-Cats-Jaguars-Tigers-Lions-Panthers-Servals-Leopards_2438808957.webp"
                    alt="Wild Animal">

                <div class="image-title">
                    Wild Animal
                </div>

            </div>

        </div>

    </div>


    <!-- ==============================
         LIGHTBOX
    ============================== -->

    <div class="lightbox" id="lightbox">


        <!-- Close button -->

        <span
            class="close-btn"
            id="closeBtn">
            &times;
        </span>


        <!-- Previous button -->

        <button
            class="nav-btn prev"
            id="prevBtn">
            &#10094;
        </button>


        <!-- Large image -->

        <img
            id="lightboxImage"
            src=""
            alt="Large Image">


        <!-- Next button -->

        <button
            class="nav-btn next"
            id="nextBtn">
            &#10095;
        </button>

    </div>



    <script>

        /* =================================
           GET HTML ELEMENTS
        ================================= */

        const galleryItems =
            document.querySelectorAll(".gallery-item");

        const lightbox =
            document.getElementById("lightbox");

        const lightboxImage =
            document.getElementById("lightboxImage");

        const closeBtn =
            document.getElementById("closeBtn");

        const prevBtn =
            document.getElementById("prevBtn");

        const nextBtn =
            document.getElementById("nextBtn");

        const filterButtons =
            document.querySelectorAll(".filter-btn");


        /* =================================
           STORE ALL IMAGE PATHS
        ================================= */

        const images = [

            "images/nature1.jpg",

            "images/nature2.jpg",

            "images/city1.jpg",

            "images/city2.jpg",

            "images/animals1.jpg",

            "images/animals2.jpg"

        ];


        /* =================================
           CURRENT IMAGE NUMBER
        ================================= */

        let currentIndex = 0;


        /* =================================
           OPEN LIGHTBOX
        ================================= */

        galleryItems.forEach(function(item) {

            item.addEventListener("click", function() {

                currentIndex =
                    Number(item.dataset.index);

                showImage();

                lightbox.classList.add("active");

            });

        });


        /* =================================
           SHOW IMAGE IN LIGHTBOX
        ================================= */

        function showImage() {

            lightboxImage.src =
                images[currentIndex];

        }


        /* =================================
           NEXT IMAGE
        ================================= */

        nextBtn.addEventListener(
            "click",
            function(event) {

                event.stopPropagation();

                currentIndex++;

                if (currentIndex >= images.length) {
                    currentIndex = 0;
                }

                showImage();

            }
        );


        /* =================================
           PREVIOUS IMAGE
        ================================= */

        prevBtn.addEventListener(
            "click",
            function(event) {

                event.stopPropagation();

                currentIndex--;

                if (currentIndex < 0) {
                    currentIndex = images.length - 1;
                }

                showImage();

            }
        );


        /* =================================
           CLOSE LIGHTBOX
        ================================= */

        closeBtn.addEventListener(
            "click",
            function() {

                lightbox.classList.remove("active");

            }
        );


        /* =================================
           CLICK OUTSIDE IMAGE TO CLOSE
        ================================= */

        lightbox.addEventListener(
            "click",
            function(event) {

                if (event.target === lightbox) {

                    lightbox.classList.remove(
                        "active"
                    );

                }

            }
        );


        /* =================================
           FILTER IMAGES
        ================================= */

        filterButtons.forEach(function(button) {

            button.addEventListener(
                "click",
                function() {

                    /* Remove active class
                       from all buttons */

                    filterButtons.forEach(
                        function(btn) {

                            btn.classList.remove(
                                "active"
                            );

                        }
                    );


                    /* Add active class
                       to clicked button */

                    button.classList.add("active");


                    /* Get selected category */

                    const filter =
                        button.dataset.filter;


                    /* Show / hide images */

                    galleryItems.forEach(
                        function(item) {

                            const category =
                                item.dataset.category;


                            if (
                                filter === "all" ||
                                filter === category
                            ) {

                                item.style.display =
                                    "block";

                            } else {

                                item.style.display =
                                    "none";

                            }

                        }
                    );

                }
            );

        });


        /* =================================
           KEYBOARD NAVIGATION
        ================================= */

        document.addEventListener(
            "keydown",
            function(event) {

                /* Escape = Close */

                if (event.key === "Escape") {

                    lightbox.classList.remove(
                        "active"
                    );

                }


                /* Right Arrow = Next */

                if (
                    event.key === "ArrowRight" &&
                    lightbox.classList.contains("active")
                ) {

                    currentIndex++;

                    if (
                        currentIndex >= images.length
                    ) {

                        currentIndex = 0;

                    }

                    showImage();

                }


                /* Left Arrow = Previous */

                if (
                    event.key === "ArrowLeft" &&
                    lightbox.classList.contains("active")
                ) {

                    currentIndex--;

                    if (currentIndex < 0) {

                        currentIndex =
                            images.length - 1;

                    }

                    showImage();

                }

            }
        );

    </script>

</body>

</html>
