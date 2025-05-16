import random
import math

class Neutron:
    def __init__(self, energy):
        self.energy = energy  # انرژی اولیه نوترون (MeV)
        self.alive = True
        self.position = 0.0  # موقعیت نوترون در ماده (سانتی‌متر)
        self.direction = 1   # جهت حرکت (1 به جلو، -1 به عقب)

    def move(self, distance):
        self.position += distance * self.direction

    def interact(self):
        # احتمال برخورد با هسته اورانیوم و شکاف هسته‌ای
        # تابعی از انرژی نوترون (مثلاً بیشتر انرژی، احتمال بیشتر)
        fission_cross_section = 0.5 * math.exp(-self.energy / 2.0)  # ساده‌شده
        interaction_prob = min(fission_cross_section, 1.0)

        if random.random() < interaction_prob:
            # شکاف هسته‌ای اتفاق می‌افتد
            self.alive = False
            print(f"شکاف هسته‌ای در موقعیت {self.position:.2f} سانتی‌متر رخ داد.")
            return True
        else:
            # نوترون بدون واکنش ادامه می‌دهد
            step = random.uniform(0.1, 1.0)  # فاصله حرکت تا برخورد بعدی
            self.move(step)
            print(f"نوترون در موقعیت {self.position:.2f} سانتی‌متر بدون واکنش حرکت کرد.")
            return False

def simulate_neutron_transport(n_neutrons):
    for i in range(n_neutrons):
        energy = random.uniform(0.1, 5.0)  # انرژی نوترون بین 0.1 تا 5 مگاالکترون‌ولت
        neutron = Neutron(energy)
        print(f"نوترون شماره {i+1} با انرژی اولیه {energy:.2f} MeV آغاز شد.")
        while neutron.alive and neutron.position < 10.0:
            neutron.interact()
        if neutron.alive:
            print("نوترون از ماده خارج شد بدون واکنش.")
        print("-" * 40)

if __name__ == "__main__":
    simulate_neutron_transport(3)
