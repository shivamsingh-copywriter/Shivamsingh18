<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shivam Singh - 3D Copywriting Portfolio</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/ScrollTrigger.min.js"></script>
    <style>
        :root {
            --primary: #ff6b35;
            --primary-dark: #e55a29;
            --secondary: #8a2be2;
            --tertiary: #00c9ff;
            --dark: #0a0a1a;
            --darker: #050510;
            --light: #f0f0f5;
            --gradient-primary: linear-gradient(135deg, var(--primary), #ff4d94);
            --gradient-secondary: linear-gradient(135deg, var(--secondary), #5d00ff);
            --gradient-tertiary: linear-gradient(135deg, var(--tertiary), #0095ff);
            --gradient-dark: linear-gradient(135deg, var(--darker), #1a1a3a);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Montserrat', 'Arial', sans-serif;
            line-height: 1.7;
            color: var(--light);
            background: var(--darker);
            overflow-x: hidden;
            perspective: 1000px;
            transform-style: preserve-3d;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 40px;
        }

        /* Header - Enhanced 3D Effect */
        header {
            background: rgba(10, 10, 26, 0.95);
            padding: 1rem 0;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            backdrop-filter: blur(12px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            transform: translateZ(20px);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: 900;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .nav-links {
            display: flex;
            list-style: none;
            gap: 3rem;
        }

        .nav-links a {
            color: var(--light);
            text-decoration: none;
            font-weight: 600;
            position: relative;
            transition: all 0.4s;
            padding: 8px 0;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 3px;
            background: var(--gradient-primary);
            border-radius: 3px;
            transition: width 0.4s ease;
        }

        .nav-links a:hover {
            color: var(--primary);
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        /* Hero Section - 3D Particles Background */
        .hero {
            background: var(--gradient-dark);
            color: white;
            text-align: center;
            padding: 180px 0 120px;
            position: relative;
            overflow: hidden;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            transform-style: preserve-3d;
        }

        #particles-js {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
        }

        .hero-content {
            position: relative;
            z-index: 2;
            transform: translateZ(50px);
            max-width: 900px;
            margin: 0 auto;
        }

        .hero h1 {
            font-size: 4.5rem;
            margin-bottom: 1.5rem;
            background: linear-gradient(45deg, #ff6b35, #f9d423, #ff6b35);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 0 20px rgba(255, 107, 53, 0.4);
            animation: glow 3s ease-in-out infinite alternate;
            line-height: 1.2;
            letter-spacing: -1px;
            transform: translateZ(40px);
        }

        @keyframes glow {
            0% { text-shadow: 0 0 10px rgba(255, 107, 53, 0.4); }
            100% { text-shadow: 0 0 30px rgba(255, 107, 53, 0.8), 
                           0 0 60px rgba(255, 107, 53, 0.6); }
        }

        .hero p {
            font-size: 1.5rem;
            margin-bottom: 3rem;
            opacity: 0.9;
            font-weight: 300;
            max-width: 700px;
            margin: 0 auto 3rem;
            transform: translateZ(30px);
        }

        .cta-button {
            display: inline-block;
            background: var(--gradient-primary);
            color: white;
            padding: 18px 50px;
            text-decoration: none;
            border-radius: 50px;
            font-weight: 700;
            font-size: 1.1rem;
            transition: all 0.4s;
            box-shadow: 0 15px 40px rgba(255, 107, 53, 0.4);
            text-transform: uppercase;
            letter-spacing: 1px;
            position: relative;
            overflow: hidden;
            z-index: 1;
            transform: translateZ(30px);
            border: none;
            cursor: pointer;
        }

        .cta-button::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--gradient-secondary);
            z-index: -1;
            opacity: 0;
            transition: opacity 0.4s;
        }

        .cta-button:hover {
            transform: translateY(-5px) scale(1.05) translateZ(30px);
            box-shadow: 0 20px 50px rgba(255, 107, 53, 0.6);
        }

        .cta-button:hover::before {
            opacity: 1;
        }

        /* About Section - 3D Card Effect */
        .about {
            background: linear-gradient(to bottom, var(--darker), #1a1a3a);
            padding: 150px 0 100px;
            position: relative;
            transform-style: preserve-3d;
        }

        .about::before {
            content: '';
            position: absolute;
            top: -100px;
            left: 0;
            right: 0;
            height: 100px;
            background: linear-gradient(to bottom, transparent, var(--darker));
        }

        .about-content {
            text-align: center;
            max-width: 1000px;
            margin: 0 auto;
            padding-top: 50px;
            transform: translateZ(40px);
        }

        .profile-container {
            position: relative;
            display: inline-block;
            margin-bottom: 3rem;
            transform-style: preserve-3d;
        }

        .profile-image {
            width: 220px;
            height: 220px;
            border-radius: 50%;
            object-fit: cover;
            border: 5px solid transparent;
            background: var(--gradient-primary) border-box;
            box-shadow: 0 20px 50px rgba(255, 107, 53, 0.3);
            transition: all 0.5s ease;
            position: relative;
            z-index: 2;
        }

        .profile-image:hover {
            transform: scale(1.05) rotateY(10deg);
            box-shadow: 0 30px 60px rgba(255, 107, 53, 0.5);
        }

        .about h2 {
            font-size: 3rem;
            margin-bottom: 2.5rem;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 0 15px rgba(255, 107, 53, 0.3);
            transform: translateZ(30px);
        }

        .about p {
            font-size: 1.25rem;
            margin-bottom: 1.8rem;
            color: #ddd;
            line-height: 1.8;
            transform: translateZ(20px);
        }

        .about-features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-top: 3rem;
            transform: translateZ(30px);
        }

        .feature {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            padding: 2rem;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            transform-style: preserve-3d;
            transition: all 0.4s;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }

        .feature:hover {
            transform: translateY(-10px) translateZ(20px);
            background: rgba(255, 107, 53, 0.1);
            box-shadow: 0 20px 50px rgba(255, 107, 53, 0.3);
        }

        .feature i {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .feature h3 {
            font-size: 1.5rem;
            margin-bottom: 1rem;
            color: white;
        }

        /* Services Section - 3D Flip Cards */
        .services {
            background: var(--gradient-dark);
            padding: 150px 0;
            position: relative;
            overflow: hidden;
            transform-style: preserve-3d;
        }

        .services::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at center, rgba(139, 0, 255, 0.1) 0%, transparent 70%);
            pointer-events: none;
        }

        .services h2 {
            text-align: center;
            font-size: 3rem;
            margin-bottom: 1rem;
            background: var(--gradient-secondary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            transform: translateZ(40px);
        }

        .services .subtitle {
            text-align: center;
            font-size: 1.3rem;
            color: #bbb;
            max-width: 800px;
            margin: 0 auto 4rem;
            transform: translateZ(30px);
        }

        .services-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 3rem;
            margin-top: 3rem;
            transform: translateZ(30px);
        }

        .service-card {
            background: rgba(20, 20, 40, 0.7);
            padding: 0;
            border-radius: 20px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
            transition: all 0.4s;
            transform-style: preserve-3d;
            perspective: 1000px;
            height: 400px;
            cursor: pointer;
        }

        .service-card-inner {
            position: relative;
            width: 100%;
            height: 100%;
            text-align: center;
            transition: transform 0.8s;
            transform-style: preserve-3d;
            border-radius: 20px;
        }

        .service-card:hover .service-card-inner {
            transform: rotateY(180deg);
        }

        .service-card-front, .service-card-back {
            position: absolute;
            width: 100%;
            height: 100%;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
            border-radius: 20px;
            padding: 2.5rem;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        .service-card-front {
            background: rgba(30, 30, 60, 0.8);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .service-card-back {
            background: var(--gradient-secondary);
            transform: rotateY(180deg);
        }

        .service-card h3 {
            color: white;
            margin-bottom: 1.5rem;
            font-size: 1.8rem;
        }

        .service-card p {
            color: #ddd;
            line-height: 1.8;
        }

        .service-icon {
            font-size: 3rem;
            margin-bottom: 1.5rem;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .service-card-back h3 {
            color: white;
            margin-bottom: 1.5rem;
        }

        .service-card-back p {
            color: rgba(255, 255, 255, 0.9);
        }

        /* Portfolio Section - 3D Gallery */
        .portfolio {
            background: var(--gradient-dark);
            color: white;
            padding: 150px 0;
            text-align: center;
            position: relative;
            transform-style: preserve-3d;
        }

        .portfolio::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><pattern id="grid" width="10" height="10" patternUnits="userSpaceOnUse"><path d="M 10 0 L 0 0 0 10" fill="none" stroke="rgba(139, 0, 255, 0.2)" stroke-width="0.5"/></pattern></defs><rect width="100" height="100" fill="url(%23grid)"/></svg>');
            opacity: 0.3;
        }

        .portfolio h2 {
            font-size: 3rem;
            margin-bottom: 1rem;
            background: var(--gradient-tertiary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            transform: translateZ(40px);
        }

        .portfolio .subtitle {
            font-size: 1.3rem;
            margin-bottom: 3rem;
            color: #bbb;
            max-width: 800px;
            margin: 0 auto 4rem;
            transform: translateZ(30px);
        }

        .portfolio-gallery {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2.5rem;
            margin: 3rem auto;
            max-width: 1400px;
            transform: translateZ(30px);
            transform-style: preserve-3d;
        }

        .portfolio-item {
            background: rgba(30, 30, 60, 0.7);
            border-radius: 15px;
            overflow: hidden;
            transform-style: preserve-3d;
            transition: all 0.5s;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
            height: 300px;
            position: relative;
        }

        .portfolio-item:hover {
            transform: translateY(-15px) rotateX(5deg) rotateY(5deg) scale(1.05);
            box-shadow: 0 25px 60px rgba(0, 195, 255, 0.3);
        }

        .portfolio-image {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: all 0.5s;
        }

        .portfolio-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(to bottom, rgba(0, 201, 255, 0.7), rgba(138, 43, 226, 0.8));
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            opacity: 0;
            transition: opacity 0.5s;
            padding: 2rem;
        }

        .portfolio-item:hover .portfolio-overlay {
            opacity: 1;
        }

        .portfolio-item h3 {
            font-size: 1.8rem;
            margin-bottom: 1rem;
            color: white;
        }

        /* Contact Section - 3D Form */
        .contact {
            background: var(--gradient-dark);
            padding: 150px 0;
            position: relative;
            transform-style: preserve-3d;
        }

        .contact h2 {
            text-align: center;
            font-size: 3rem;
            margin-bottom: 1rem;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            transform: translateZ(40px);
        }

        .contact .subtitle {
            text-align: center;
            font-size: 1.3rem;
            margin-bottom: 4rem;
            color: #bbb;
            max-width: 800px;
            margin: 0 auto;
            transform: translateZ(30px);
        }

        .contact-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            max-width: 1400px;
            margin: 0 auto;
            transform: translateZ(30px);
        }

        .contact-info {
            background: rgba(30, 30, 60, 0.7);
            border-radius: 20px;
            padding: 3rem;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transform: translateZ(20px);
        }

        .contact-info h3 {
            font-size: 2rem;
            margin-bottom: 2rem;
            color: var(--primary);
        }

        .contact-details {
            margin-bottom: 3rem;
        }

        .contact-detail {
            display: flex;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .contact-detail i {
            font-size: 1.5rem;
            margin-right: 1rem;
            color: var(--primary);
            width: 40px;
            height: 40px;
            background: rgba(255, 107, 53, 0.1);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .social-contact {
            display: flex;
            gap: 1.5rem;
        }

        .social-contact a {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: var(--gradient-primary);
            color: white;
            font-size: 1.5rem;
            transition: all 0.3s;
        }

        .social-contact a:hover {
            transform: translateY(-5px) scale(1.1);
        }

        .contact-form {
            background: rgba(30, 30, 60, 0.7);
            padding: 3rem;
            border-radius: 20px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transform: translateZ(20px);
        }

        .form-group {
            margin-bottom: 1.8rem;
            transform: translateZ(10px);
        }

        .form-group label {
            display: block;
            margin-bottom: 0.8rem;
            font-weight: 600;
            color: #ddd;
        }

        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 15px;
            border: none;
            border-radius: 10px;
            font-size: 1rem;
            background: rgba(10, 10, 26, 0.7);
            color: white;
            transition: all 0.3s;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 15px rgba(255, 107, 53, 0.3);
        }

        .submit-btn {
            width: 100%;
            background: var(--gradient-primary);
            color: white;
            padding: 18px;
            border: none;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.4s;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-top: 1rem;
        }

        .submit-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(255, 107, 53, 0.4);
        }

        /* Newsletter Section - 3D Effect */
        .newsletter {
            background: var(--gradient-secondary);
            color: white;
            padding: 100px 0;
            text-align: center;
            position: relative;
            overflow: hidden;
            transform-style: preserve-3d;
        }

        .newsletter::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><pattern id="diamond" width="10" height="10" patternUnits="userSpaceOnUse"><path d="M 0,5 L 5,0 10,5 5,10 Z" fill="none" stroke="rgba(255,255,255,0.2)" stroke-width="0.5"/></pattern></defs><rect width="100" height="100" fill="url(%23diamond)"/></svg>');
            opacity: 0.2;
        }

        .newsletter h3 {
            font-size: 2.5rem;
            margin-bottom: 1.5rem;
            transform: translateZ(40px);
        }

        .newsletter p {
            font-size: 1.3rem;
            margin-bottom: 3rem;
            max-width: 700px;
            margin: 0 auto 3rem;
            transform: translateZ(30px);
            opacity: 0.9;
        }

        .newsletter-form {
            max-width: 500px;
            margin: 0 auto;
            display: flex;
            gap: 1rem;
            transform: translateZ(30px);
        }

        .newsletter-form input {
            flex: 1;
            padding: 15px 20px;
            border: none;
            border-radius: 50px;
            font-size: 1rem;
            background: rgba(255, 255, 255, 0.15);
            color: white;
            transition: all 0.3s;
        }

        .newsletter-form input:focus {
            outline: none;
            background: rgba(255, 255, 255, 0.25);
            box-shadow: 0 0 20px rgba(255, 255, 255, 0.2);
        }

        .newsletter-form input::placeholder {
            color: rgba(255, 255, 255, 0.7);
        }

        .newsletter-btn {
            background: var(--gradient-primary);
            color: white;
            padding: 15px 35px;
            border: none;
            border-radius: 50px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.4s;
            font-size: 1rem;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .newsletter-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
        }

        /* Footer */
        footer {
            background: var(--darker);
            color: white;
            text-align: center;
            padding: 4rem 0 2rem;
            position: relative;
            transform-style: preserve-3d;
        }

        .footer-content {
            max-width: 800px;
            margin: 0 auto 3rem;
            transform: translateZ(30px);
        }

        .footer-logo {
            font-size: 2.5rem;
            font-weight: 900;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 1.5rem;
            text-transform: uppercase;
            letter-spacing: 3px;
        }

        .footer-tagline {
            font-size: 1.3rem;
            margin-bottom: 2rem;
            color: #bbb;
        }

        .social-links {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin-bottom: 3rem;
        }

        .social-links a {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: var(--gradient-primary);
            color: white;
            font-size: 1.8rem;
            transition: all 0.4s;
            text-decoration: none;
        }

        .social-links a:hover {
            transform: translateY(-8px) scale(1.1);
            box-shadow: 0 10px 25px rgba(255, 107, 53, 0.4);
        }

        .copyright {
            padding-top: 2rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            color: #777;
            font-size: 1.1rem;
        }

        /* Scroll to Top */
        .scroll-top {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 60px;
            height: 60px;
            background: var(--gradient-primary);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            cursor: pointer;
            z-index: 999;
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.4s;
            box-shadow: 0 5px 15px rgba(255, 107, 53, 0.4);
        }

        .scroll-top.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .scroll-top:hover {
            transform: translateY(-5px) scale(1.1);
            box-shadow: 0 10px 25px rgba(255, 107, 53, 0.6);
        }

        /* Responsive */
        @media (max-width: 1200px) {
            .container {
                padding: 0 30px;
            }
            
            .hero h1 {
                font-size: 3.8rem;
            }
            
            .contact-container {
                grid-template-columns: 1fr;
                gap: 3rem;
            }
        }

        @media (max-width: 992px) {
            .hero h1 {
                font-size: 3.2rem;
            }
            
            .nav-links {
                gap: 2rem;
            }
            
            .services-grid {
                grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            }
        }

        @media (max-width: 768px) {
            .hero {
                padding: 150px 0 80px;
            }
            
            .hero h1 {
                font-size: 2.8rem;
            }
            
            .hero p {
                font-size: 1.2rem;
            }
            
            .nav-links {
                display: none;
            }
            
            .mobile-menu-btn {
                display: block;
                font-size: 1.8rem;
                color: white;
                background: none;
                border: none;
                cursor: pointer;
            }
            
            .newsletter-form {
                flex-direction: column;
            }
            
            .portfolio-gallery {
                grid-template-columns: 1fr;
            }
            
            .about-features {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 576px) {
            .container {
                padding: 0 20px;
            }
            
            .hero h1 {
                font-size: 2.2rem;
            }
            
            .cta-button {
                padding: 15px 30px;
                font-size: 1rem;
            }
            
            .about h2, .services h2, .portfolio h2, .contact h2 {
                font-size: 2.2rem;
            }
        }

        /* Animation Classes */
        .fade-in {
            opacity: 0;
            transform: translateY(30px) translateZ(20px);
            transition: all 0.8s ease-out;
        }

        .fade-in.visible {
            opacity: 1;
            transform: translateY(0) translateZ(0);
        }

        /* 3D Elements */
        .floating {
            animation: floating 6s ease-in-out infinite;
        }

        @keyframes floating {
            0% { transform: translateY(0) translateZ(20px); }
            50% { transform: translateY(-20px) translateZ(30px); }
            100% { transform: translateY(0) translateZ(20px); }
        }

        .rotate-3d {
            animation: rotate3d 20s linear infinite;
            transform-style: preserve-3d;
        }

        @keyframes rotate3d {
            0% { transform: rotateY(0deg) rotateX(0deg); }
            100% { transform: rotateY(360deg) rotateX(360deg); }
        }
    </style>
</head>
<body>
    <!-- Particles Container -->
    <div id="particles-js"></div>
    
    <!-- Scroll to Top Button -->
    <div class="scroll-top">
        <i class="fas fa-arrow-up"></i>
    </div>
    
    <header>
        <nav class="container">
            <div class="logo">Shivam Singh</div>
            <ul class="nav-links">
                <li><a href="#about">About</a></li>
                <li><a href="#services">Services</a></li>
                <li><a href="#portfolio">Portfolio</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
            <button class="mobile-menu-btn">
                <i class="fas fa-bars"></i>
            </button>
        </nav>
    </header>

    <section class="hero">
        <div class="container">
            <div class="hero-content">
                <h1 class="fade-in floating">WORDS THAT WORK. COPY THAT CLICKS. STRATEGY THAT SELLS.</h1>
                <p class="fade-in">I write conversion-focused copy for online fitness trainers who are done with guesswork — and ready to get results.</p>
                <a href="#portfolio" class="cta-button fade-in">VIEW MY WORK</a>
            </div>
        </div>
    </section>

    <section class="about" id="about">
        <div class="container">
            <div class="about-content">
                <div class="profile-container fade-in">
                    <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80" alt="Shivam Singh - Copywriter" class="profile-image">
                </div>
                
                <h2 class="fade-in">COPY THAT FEELS LIKE YOU. SELLS LIKE NEVER BEFORE.</h2>
                <p class="fade-in">I'm Shivam, a conversion strategist and a copywriter. I help online fitness trainers turn scrollers into buyers with conversion copy that doesn't just "sound good" but also sells.</p>
                
                <p class="fade-in">My words have launched 6-figure funnels, doubled course sales, and rewritten dusty brand messaging into revenue engines.</p>
                
                <p class="fade-in">But this isn't just about fancy numbers.</p>
                
                <p class="fade-in">Because if your copy isn't converting, it's not a you problem. It's a messaging problem.</p>
                
                <p class="fade-in"><strong>I can change your copy into money-making machines.</strong></p>
                
                <div class="about-features">
                    <div class="feature fade-in">
                        <i class="fas fa-comments"></i>
                        <h3>Voice-of-customer research</h3>
                        <p>So your audience feels seen and understood</p>
                    </div>
                    
                    <div class="feature fade-in">
                        <i class="fas fa-brain"></i>
                        <h3>Psychology-backed structure</h3>
                        <p>Compelling content that keeps readers engaged</p>
                    </div>
                    
                    <div class="feature fade-in">
                        <i class="fas fa-gem"></i>
                        <h3>Irresistible offers</h3>
                        <p>Creating value that converts without being pushy</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section class="services" id="services">
        <div class="container">
            <h2 class="fade-in">NO TEMPLATES. NO GUESSWORK. JUST COPY THAT CONVERTS.</h2>
            <p class="fade-in subtitle">If you're tired of AI-generated fluff, bro-marketing BS, or hiring "just a writer" who doesn't understand strategy — you're in the right place. I don't write words to fill space. I write to drive sales.</p>
            
            <div class="services-grid">
                <div class="service-card fade-in">
                    <div class="service-card-inner">
                        <div class="service-card-front">
                            <div class="service-icon">
                                <i class="fas fa-file-alt"></i>
                            </div>
                            <h3>Sales Pages That Sell More Without Sounding Salesy</h3>
                            <p>Crafted to tap into desire, crush objections, and make the "Buy Now" button too tempting to ignore.</p>
                        </div>
                        <div class="service-card-back">
                            <h3>Results You Can Expect</h3>
                            <p>20-50% increase in conversion rates. Compelling storytelling that builds trust and drives action.</p>
                        </div>
                    </div>
                </div>
                
                <div class="service-card fade-in">
                    <div class="service-card-inner">
                        <div class="service-card-front">
                            <div class="service-icon">
                                <i class="fas fa-envelope"></i>
                            </div>
                            <h3>Email Sequences That Nurture and Convert</h3>
                            <p>Build trust. Prime buyers. Drive action. On autopilot.</p>
                        </div>
                        <div class="service-card-back">
                            <h3>Results You Can Expect</h3>
                            <p>30-70% open rates. 3-8% CTR. Automated revenue streams that convert subscribers into buyers.</p>
                        </div>
                    </div>
                </div>
                
                <div class="service-card fade-in">
                    <div class="service-card-inner">
                        <div class="service-card-front">
                            <div class="service-icon">
                                <i class="fas fa-globe"></i>
                            </div>
                            <h3>Website Copy That Tells Your Story (and Sells It)</h3>
                            <p>Because your homepage should work as hard as your best closer.</p>
                        </div>
                        <div class="service-card-back">
                            <h3>Results You Can Expect</h3>
                            <p>Higher engagement and lower bounce rates. Clear messaging that converts visitors into leads.</p>
                        </div>
                    </div>
                </div>
                
                <div class="service-card fade-in">
                    <div class="service-card-inner">
                        <div class="service-card-front">
                            <div class="service-icon">
                                <i class="fas fa-rocket"></i>
                            </div>
                            <h3>Launch Strategy + Messaging</h3>
                            <p>From pre-launch buzz to cart-close urgency — I help you plan, write, and execute with clarity.</p>
                        </div>
                        <div class="service-card-back">
                            <h3>Results You Can Expect</h3>
                            <p>Successful product launches. Strategic messaging that creates anticipation and drives sales.</p>
                        </div>
                    </div>
                </div>
                
                <div class="service-card fade-in">
                    <div class="service-card-inner">
                        <div class="service-card-front">
                            <div class="service-icon">
                                <i class="fas fa-ad"></i>
                            </div>
                            <h3>Social Media Ads for Brand Awareness</h3>
                            <p>Because most of the traffic will come from social media.</p>
                        </div>
                        <div class="service-card-back">
                            <h3>Results You Can Expect</h3>
                            <p>Higher CTR and lower CAC. Ads that stand out and drive targeted traffic to your offers.</p>
                        </div>
                    </div>
                </div>
                
                <div class="service-card fade-in">
                    <div class="service-card-inner">
                        <div class="service-card-front">
                            <div class="service-icon">
                                <i class="fas fa-plus-circle"></i>
                            </div>
                            <h3>Optional Add-Ons</h3>
                            <p>Funnel Audits | Offer Positioning | Social media copy for organic growth</p>
                        </div>
                        <div class="service-card-back">
                            <h3>Results You Can Expect</h3>
                            <p>Optimized funnels that convert better. Strategic positioning that differentiates your offer.</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section class="portfolio" id="portfolio">
        <div class="container">
            <h2 class="fade-in">COPY THAT MOVES THE NEEDLE (AND THE REVENUE METER)</h2>
            <p class="fade-in subtitle">I don't believe in "pretty words." I believe in performance. Have a look at my copies.</p>
            
            <div class="portfolio-gallery">
                <div class="portfolio-item fade-in">
                    <img src="https://images.unsplash.com/photo-1551434678-e076c223a692?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1770&q=80" alt="Sales Page" class="portfolio-image">
                    <div class="portfolio-overlay">
                        <h3>SALES PAGE</h3>
                        <p>High-converting sales pages that drive action</p>
                    </div>
                </div>
                
                <div class="portfolio-item fade-in">
                    <img src="https://images.unsplash.com/photo-1499951360447-b19be8fe80f5?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1770&q=80" alt="Landing Page" class="portfolio-image">
                    <div class="portfolio-overlay">
                        <h3>LANDING PAGE</h3>
                        <p>Targeted landing pages that convert visitors</p>
                    </div>
                </div>
                
                <div class="portfolio-item fade-in">
                    <img src="https://images.unsplash.com/photo-1551836022-d5d88e9218df?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1770&q=80" alt="Optin Pages" class="portfolio-image">
                    <div class="portfolio-overlay">
                        <h3>OPTIN PAGES</h3>
                        <p>Lead capture pages that build your email list</p>
                    </div>
                </div>
                
                <div class="portfolio-item fade-in">
                    <img src="https://images.unsplash.com/photo-1519241047957-be2f8036f3b1?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1770&q=80" alt="Emails" class="portfolio-image">
                    <div class="portfolio-overlay">
                        <h3>EMAILS</h3>
                        <p>Engaging email sequences that nurture leads</p>
                    </div>
                </div>
                
                <div class="portfolio-item fade-in">
                    <img src="https://images.unsplash.com/photo-1563986768609-322da13575f3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1770&q=80" alt="Ads" class="portfolio-image">
                    <div class="portfolio-overlay">
                        <h3>ADS</h3>
                        <p>High-performing ad copy that drives clicks</p>
                    </div>
                </div>
                
                <div class="portfolio-item fade-in">
                    <img src="https://images.unsplash.com/photo-1611162617474-5b21e879e113?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1674&q=80" alt="Social Media Copies" class="portfolio-image">
                    <div class="portfolio-overlay">
                        <h3>SOCIAL MEDIA COPIES</h3>
                        <p>Engaging social content that builds community</p>
                    </div>
                </div>
            </div>
            
            <div class="fade-in" style="margin-top: 4rem;">
                <h3>Ready for Copy That Converts, Closes, and Compels?</h3>
                <a href="#contact" class="cta-button" style="margin-top: 2rem;">LET'S WORK TOGETHER</a>
            </div>
        </div>
    </section>

    <section class="contact" id="contact">
        <div class="container">
            <h2 class="fade-in">Let's Build Something That Converts</h2>
            <p class="fade-in subtitle">Let's turn your offer into a no-brainer. Tell me a bit about what you need, and I'll be in touch with next steps.</p>
            
            <div class="contact-container">
                <div class="contact-info fade-in">
                    <h3>Get In Touch</h3>
                    <div class="contact-details">
                        <div class="contact-detail">
                            <i class="fas fa-envelope"></i>
                            <div>
                                <h4>Email</h4>
                                <p>shivamthemarketer@gmail.com</p>
                            </div>
                        </div>
                        
                        <div class="contact-detail">
                            <i class="fas fa-map-marker-alt"></i>
                            <div>
                                <h4>Based In</h4>
                                <p>India, Serving Worldwide</p>
                            </div>
                        </div>
                        
                        <div class="contact-detail">
                            <i class="fas fa-clock"></i>
                            <div>
                                <h4>Availability</h4>
                                <p>Monday - Friday: 9AM - 6PM</p>
                            </div>
                        </div>
                    </div>
                    
                    <h3>Connect With Me</h3>
                    <div class="social-contact">
                        <a href="https://instagram.com/yourusername" target="_blank"><i class="fab fa-instagram"></i></a>
                        <a href="https://twitter.com/yourusername" target="_blank"><i class="fab fa-twitter"></i></a>
                        <a href="https://linkedin.com/in/yourusername" target="_blank"><i class="fab fa-linkedin-in"></i></a>
                    </div>
                </div>
                
                <form class="contact-form fade-in" action="https://formspree.io/f/xpwaanek" method="POST">
                    <div class="form-group">
                        <label for="name">Name</label>
                        <input type="text" id="name" name="name" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="email">Email</label>
                        <input type="email" id="email" name="email" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="website">Brand/Website</label>
                        <input type="text" id="website" name="website">
                    </div>
                    
                    <div class="form-group">
                        <label for="service">Service Needed</label>
                        <select id="service" name="service" required>
                            <option value="">Select a service</option>
                            <option value="sales-page">Sales Page</option>
                            <option value="email-sequence">Email Sequence</option>
                            <option value="website-copy">Website Copy</option>
                            <option value="launch-strategy">Launch Strategy</option>
                            <option value="social-ads">Social Media Ads</option>
                            <option value="other">Other</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="needs">What do you need?</label>
                        <textarea id="needs" name="needs" rows="5" placeholder="Tell me about your project, goals, and challenges..." required></textarea>
                    </div>
                    
                    <button type="submit" class="submit-btn">Let's Do This</button>
                </form>
            </div>
        </div>
    </section>

    <section class="newsletter">
        <div class="container">
            <h3 class="fade-in">Steal My Secrets (Ethically)</h3>
            <p class="fade-in">Get inside my swipe file — and my brain. No spam. Just actionable copy and conversion tips you'll actually use.</p>
            
            <form class="newsletter-form fade-in" action="https://formspree.io/f/xpwaanek" method="POST">
                <input type="email" name="newsletter_email" placeholder="Your email address" required>
                <input type="hidden" name="form_type" value="newsletter">
                <button type="submit" class="newsletter-btn">Send Me the Goods</button>
            </form>
        </div>
    </section>

    <footer>
        <div class="container">
            <div class="footer-content fade-in">
                <div class="footer-logo">Shivam Singh</div>
                <p class="footer-tagline">Conversion Copywriter & Strategy for Fitness Professionals</p>
                
                <div class="social-links">
                    <a href="mailto:shivamthemarketer@gmail.com"><i class="fas fa-envelope"></i></a>
                    <a href="https://instagram.com/yourusername" target="_blank"><i class="fab fa-instagram"></i></a>
                    <a href="https://linkedin.com/in/yourusername" target="_blank"><i class="fab fa-linkedin-in"></i></a>
                    <a href="https://twitter.com/yourusername" target="_blank"><i class="fab fa-twitter"></i></a>
                </div>
            </div>
            <p class="copyright fade-in">&copy; 2025 Shivam Singh. All rights reserved.</p>
        </div>
    </footer>

    <script>
        // Initialize Particles.js
        document.addEventListener('DOMContentLoaded', function() {
            // Particles.js configuration
            const particlesConfig = {
                particles: {
                    number: {
                        value: 80,
                        density: {
                            enable: true,
                            value_area: 800
                        }
                    },
                    color: {
                        value: "#ff6b35"
                    },
                    shape: {
                        type: "circle",
                        stroke: {
                            width: 0,
                            color: "#000000"
                        }
                    },
                    opacity: {
                        value: 0.5,
                        random: true,
                        anim: {
                            enable: true,
                            speed: 1,
                            opacity_min: 0.1,
                            sync: false
                        }
                    },
                    size: {
                        value: 3,
                        random: true,
                        anim: {
                            enable: true,
                            speed: 2,
                            size_min: 0.3,
                            sync: false
                        }
                    },
                    line_linked: {
                        enable: true,
                        distance: 150,
                        color: "#8a2be2",
                        opacity: 0.4,
                        width: 1
                    },
                    move: {
                        enable: true,
                        speed: 1,
                        direction: "none",
                        random: true,
                        straight: false,
                        out_mode: "out",
                        bounce: false,
                        attract: {
                            enable: true,
                            rotateX: 600,
                            rotateY: 1200
                        }
                    }
                },
                interactivity: {
                    detect_on: "canvas",
                    events: {
                        onhover: {
                            enable: true,
                            mode: "grab"
                        },
                        onclick: {
                            enable: true,
                            mode: "push"
                        },
                        resize: true
                    },
                    modes: {
                        grab: {
                            distance: 140,
                            line_linked: {
                                opacity: 1
                            }
                        },
                        push: {
                            particles_nb: 4
                        }
                    }
                },
                retina_detect: true
            };

            // Load particles.js if it's not already loaded
            if (typeof particlesJS !== 'undefined') {
                particlesJS('particles-js', particlesConfig);
            } else {
                console.warn('particles.js not loaded');
            }

            // Initialize GSAP ScrollTrigger
            gsap.registerPlugin(ScrollTrigger);

            // Set up scroll animations
            gsap.utils.toArray('.fade-in').forEach(element => {
                gsap.fromTo(element, {
                    opacity: 0,
                    y: 50
                }, {
                    opacity: 1,
                    y: 0,
                    duration: 1,
                    scrollTrigger: {
                        trigger: element,
                        start: 'top 80%',
                        toggleActions: 'play none none none'
                    }
                });
            });

            // Floating animation for elements
            gsap.to('.floating', {
                y: -20,
                duration: 2,
                repeat: -1,
                yoyo: true,
                ease: 'power1.inOut'
            });

            // Smooth scrolling for navigation links
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function(e) {
                    e.preventDefault();
                    const target = document.querySelector(this.getAttribute('href'));
                    if (target) {
                        window.scrollTo({
                            top: target.offsetTop - 80,
                            behavior: 'smooth'
                        });
                    }
                });
            });

            // Scroll to top button
            const scrollTopBtn = document.querySelector('.scroll-top');
            
            window.addEventListener('scroll', () => {
                if (window.pageYOffset > 500) {
                    scrollTopBtn.classList.add('visible');
                } else {
                    scrollTopBtn.classList.remove('visible');
                }
            });
            
            scrollTopBtn.addEventListener('click', () => {
                window.scrollTo({
                    top: 0,
                    behavior: 'smooth'
                });
            });

            // Form submission feedback
            document.querySelector('.contact-form').addEventListener('submit', function(e) {
                const submitBtn = this.querySelector('.submit-btn');
                submitBtn.textContent = 'Sending...';
                submitBtn.disabled = true;
                
                setTimeout(() => {
                    submitBtn.textContent = 'Sent Successfully!';
                    setTimeout(() => {
                        submitBtn.textContent = 'Let\'s Do This';
                        submitBtn.disabled = false;
                    }, 2000);
                }, 1500);
            });

            document.querySelector('.newsletter-form').addEventListener('submit', function(e) {
                const submitBtn = this.querySelector('.newsletter-btn');
                submitBtn.textContent = 'Sending...';
                submitBtn.disabled = true;
                
                setTimeout(() => {
                    submitBtn.textContent = 'Sent Successfully!';
                    setTimeout(() => {
                        submitBtn.textContent = 'Send Me the Goods';
                        submitBtn.disabled = false;
                    }, 2000);
                }, 1500);
            });

            // Mouse move 3D effect for hero section
            const hero = document.querySelector('.hero');
            const heroContent = document.querySelector('.hero-content');
            
            if (hero && heroContent) {
                hero.addEventListener('mousemove', (e) => {
                    const xAxis = (window.innerWidth / 2 - e.pageX) / 25;
                    const yAxis = (window.innerHeight / 2 - e.pageY) / 25;
                    heroContent.style.transform = `translateZ(50px) rotateY(${xAxis}deg) rotateX(${yAxis}deg)`;
                });
                
                hero.addEventListener('mouseleave', () => {
                    heroContent.style.transform = 'translateZ(50px) rotateY(0deg) rotateX(0deg)';
                });
            }
        });
    </script>
</body>
</html>
