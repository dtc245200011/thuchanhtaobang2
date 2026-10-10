-- Tạo cơ sở dữ liệu
DROP DATABASE IF EXISTS QuanLyDiemThi;
CREATE DATABASE QuanLyDiemThi;
USE QuanLyDiemThi;

-- Bảng HocSinh
CREATE TABLE HocSinh (
    MaHS INT PRIMARY KEY,
    HoTen VARCHAR(100) NOT NULL,
    NgaySinh DATE,
    DiaChi VARCHAR(200)
);

-- Bảng MonHoc
CREATE TABLE MonHoc (
    MaMH INT PRIMARY KEY,
    TenMH VARCHAR(100) NOT NULL,
    SoTinChi INT
);

-- Bảng GiaoVien
CREATE TABLE GiaoVien (
    MaGV INT PRIMARY KEY,
    HoTenGV VARCHAR(100) NOT NULL,
    BoMon VARCHAR(100)
);

-- Bảng BangDiem (khóa chính kép + khóa ngoại)
CREATE TABLE BangDiem (
    MaHS INT,
    MaMH INT,
    DiemThi DECIMAL(4,2),
    MaGV INT,
    PRIMARY KEY (MaHS, MaMH),
    FOREIGN KEY (MaHS) REFERENCES HocSinh(MaHS),
    FOREIGN KEY (MaMH) REFERENCES MonHoc(MaMH),
    FOREIGN KEY (MaGV) REFERENCES GiaoVien(MaGV)
);

-- Ví dụ thêm khóa ngoại bằng ALTER TABLE
ALTER TABLE BangDiem
ADD CONSTRAINT fk_bangdiem_monhoc FOREIGN KEY (MaMH) REFERENCES MonHoc(MaMH);

ALTER TABLE BangDiem
ADD CONSTRAINT fk_bangdiem_hocsinh FOREIGN KEY (MaHS) REFERENCES HocSinh(MaHS);

ALTER TABLE BangDiem
ADD CONSTRAINT fk_bangdiem_giaovien FOREIGN KEY (MaGV) REFERENCES GiaoVien(MaGV);
