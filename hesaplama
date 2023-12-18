#include <iostream>
#include <gtest/gtest.h>
#include "hesap.h"  // Hesap sınıfının tanımının bulunduğu başlık dosyası

class Hesap {
private:
  long   hesapno;
  short  hesapturu; // 0: vadeli 1: vadesiz
  double bakiye;

public:
  Hesap();   // varsayılan yapılandırıcı
  double getBakiye();
  double paraYatir(double _tutar);
  double paraCek(double _tutar);
};

Hesap::Hesap() : hesapno(0), hesapturu(1), bakiye(0.0) {}

double Hesap::getBakiye() {
  return bakiye;
}

double Hesap::paraYatir(double _tutar) {
  if (_tutar > 0) {
    bakiye += _tutar;
    std::cout << "Para yatirildi. Yeni bakiye: " << bakiye << std::endl;
  } else {
    std::cout << "Gecersiz tutar. Para yatirilamadi." << std::endl;
  }
  return bakiye;
}

double Hesap::paraCek(double _tutar) {
  if (_tutar > 0 && bakiye >= _tutar) {
    bakiye -= _tutar;
    std::cout << "Para cekildi. Yeni bakiye: " << bakiye << std::endl;
  } else {
    std::cout << "Gecersiz tutar veya yetersiz bakiye. Para cekilemedi." << std::endl;
  }
  return bakiye;
}



TEST(HesapTest, ParaYatirTest) {
  Hesap hesap;
  EXPECT_EQ(0.0, hesap.getBakiye());  // Başlangıçta bakiye 0 olmalı

  hesap.paraYatir(100.0);
  EXPECT_EQ(100.0, hesap.getBakiye());  // 100 TL yatırıldığında bakiye 100 olmalı

  hesap.paraYatir(-50.0);
  EXPECT_EQ(100.0, hesap.getBakiye());  // Geçersiz tutar için bakiye değişmemeli
}

TEST(HesapTest, ParaCekTest) {
  Hesap hesap;
  hesap.paraYatir(200.0);

  hesap.paraCek(50.0);
  EXPECT_EQ(150.0, hesap.getBakiye());  // 50 TL çekildiğinde bakiye 150 olmalı

  hesap.paraCek(200.0);
  EXPECT_EQ(150.0, hesap.getBakiye());  // Yetersiz bakiye için bakiye değişmemeli

  hesap.paraCek(-30.0);
  EXPECT_EQ(150.0, hesap.getBakiye());  // Geçersiz tutar için bakiye değişmemeli
}

int main(int argc, char **argv) {
  ::testing::InitGoogleTest(&argc, argv);
  return RUN_ALL_TESTS();
}
