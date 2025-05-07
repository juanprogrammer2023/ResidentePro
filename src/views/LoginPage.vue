<template>
    <div class="login-container">
        <div class="login-header">
            <h1>Sistema de Gestión Financiera</h1>
            <p>Ingrese sus credenciales para acceder</p>
        </div>
        
        <form id="login-form">
            <div class="input-group">
                <label for="username">Usuario</label>
                <i class="fas fa-user"></i>
                <input type="text" id="username" placeholder="Ingrese su usuario" required>
                <div class="error-message" id="username-error"></div>
            </div>
            
            <div class="input-group">
                <label for="password">Contraseña</label>
                <i class="fas fa-lock"></i>
                <input type="password" id="password" placeholder="Ingrese su contraseña" required>
                <div class="error-message" id="password-error"></div>
            </div>
            
            <div class="remember-forgot">
                <div class="remember-me">
                    <input type="checkbox" id="remember">
                    <label for="remember">Recordarme</label>
                </div>
                <a href="#" class="forgot-password">¿Olvidó su contraseña?</a>
            </div>
            
            <button type="submit" class="btn-login">Iniciar sesión</button>
        </form>
    </div>
</template>

<style scoped>

* {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .login-container {
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 400px;
            padding: 2rem;
        }
        
        .login-header {
            text-align: center;
            margin-bottom: 2rem;
        }
        
        .login-header h1 {
            color: #2c3e50;
            font-size: 1.8rem;
            margin-bottom: 0.5rem;
        }
        
        .login-header p {
            color: #7f8c8d;
            font-size: 0.9rem;
        }
        
        .input-group {
            margin-bottom: 1.5rem;
            position: relative;
        }
        
        .input-group label {
            display: block;
            margin-bottom: 0.5rem;
            color: #34495e;
            font-weight: 500;
        }
        
        .input-group input {
            width: 100%;
            padding: 0.75rem 1rem 0.75rem 2.5rem;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
            transition: border 0.3s;
        }
        
        .input-group input:focus {
            outline: none;
            border-color: #3498db;
        }
        
        .input-group i {
            position: absolute;
            left: 1rem;
            top: 2.4rem;
            color: #95a5a6;
        }
        
        .remember-forgot {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
            font-size: 0.85rem;
        }
        
        .remember-me {
            display: flex;
            align-items: center;
        }
        
        .remember-me input {
            margin-right: 0.5rem;
        }
        
        .forgot-password {
            color: #3498db;
            text-decoration: none;
        }
        
        .forgot-password:hover {
            text-decoration: underline;
        }
        
        .btn-login {
            width: 100%;
            background-color: #3498db;
            color: white;
            border: none;
            padding: 0.75rem;
            border-radius: 5px;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        .btn-login:hover {
            background-color: #2980b9;
        }
        
        .error-message {
            color: #e74c3c;
            font-size: 0.85rem;
            margin-top: 0.5rem;
            display: none;
        }
        
        @media (max-width: 480px) {
            .login-container {
                width: 90%;
                padding: 1.5rem;
            }
        }
</style>