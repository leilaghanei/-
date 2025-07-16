import numpy as np
import matplotlib.pyplot as plt
from scipy.optimize import curve_fit

# مدل نمایی برای واپاشی پرتوی: A(t) = A0 * exp(-λ * t)
def decay_model(t, A0, lamb):
    return A0 * np.exp(-lamb * t)

# پارامترهای واقعی (مقدار اولیه و نرخ واپاشی)
A0_true = 1000
lamb_true = 0.1

# تولید داده‌های مصنوعی با نویز تصادفی
t_data = np.linspace(0, 50, 50)
y_data = decay_model(t_data, A0_true, lamb_true) + np.random.normal(0, 30, size=t_data.size)

# برازش منحنی با مدل نمایی
popt, pcov = curve_fit(decay_model, t_data, y_data, p0=[900, 0.05])
A0_fit, lamb_fit = popt

# محاسبه خروجی مدل و خطای میانگین مربعات (MSE)
y_fit = decay_model(t_data, A0_fit, lamb_fit)
residuals = y_data - y_fit
mse = np.mean(residuals**2)

# نمایش نتایج
print(f"برازش A0 = {A0_fit:.2f}")
print(f"برازش λ = {lamb_fit:.4f}")
print(f"میانگین خطا (MSE) = {mse:.2f}")

# رسم نمودار داده‌ها و مدل برازش‌شده
plt.figure(figsize=(10, 6))
plt.scatter(t_data, y_data, label='داده‌های تجربی', color='red')
plt.plot(t_data, y_fit, label='مدل برازش‌شده', color='blue')
plt.title('برازش منحنی واپاشی پرتوی رادیواکتیو')
plt.xlabel('زمان (ثانیه)')
plt.ylabel('فعالیت (A)')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
