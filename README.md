class Kontak:
    def __init__(self, nama, nomor):
        self.nama = nama
        self.nomor = nomor
        self.left = None
        self.right = None


class BSTKontak:
    def __init__(self):
        self.root = None

    def insert_node(self, root, nama, nomor):
        if root is None:
            return Kontak(nama, nomor)

        if nama.lower() < root.nama.lower():
            root.left = self.insert_node(root.left, nama, nomor)
        elif nama.lower() > root.nama.lower():
            root.right = self.insert_node(root.right, nama, nomor)

        return root

    def insert(self, nama, nomor):
        self.root = self.insert_node(self.root, nama, nomor)

    def search_node(self, root, nama):
        if root is None:
            return None

        if root.nama.lower() == nama.lower():
            return root

        if nama.lower() < root.nama.lower():
            return self.search_node(root.left, nama)

        return self.search_node(root.right, nama)

    def search(self, nama):
        return self.search_node(self.root, nama)

    def inorder(self, root):
        if root is None:
            return

        self.inorder(root.left)
        print(f"Nama : {root.nama} | Nomor : {root.nomor}")
        self.inorder(root.right)

    def preorder(self, root):
        if root is None:
            return

        print(f"Nama : {root.nama} | Nomor : {root.nomor}")
        self.preorder(root.left)
        self.preorder(root.right)

    def postorder(self, root):
        if root is None:
            return

        self.postorder(root.left)
        self.postorder(root.right)
        print(f"Nama : {root.nama} | Nomor : {root.nomor}")

    def count_contacts(self, root):
        if root is None:
            return 0

        return 1 + self.count_contacts(root.left) + self.count_contacts(root.right)

    def find_first_contact(self, root):
        if root is None:
            return None

        current = root
        while current.left is not None:
            current = current.left

        return current

    def find_last_contact(self, root):
        if root is None:
            return None

        current = root
        while current.right is not None:
            current = current.right

        return current

def main():
    bst = BSTKontak()
    pilih = 0

    while pilih != 8:
        print("\n=== DAFTAR KONTAK PONSEL ===")
        print("1. Tambah Kontak")
        print("2. Cari Kontak")
        print("3. Tampilkan Kontak (Inorder)")
        print("4. Preorder")
        print("5. Postorder")
        print("6. Kontak Awal")
        print("7. Jumlah Kontak")
        print("8. Keluar")

        try:
            pilih = int(input("Pilih menu: "))
        except ValueError:
            print("Input tidak valid!")
            continue

        if pilih == 1:
            nama = input("Masukkan nama kontak : ")
            nomor = input("Masukkan nomor HP    : ")

            bst.insert(nama, nomor)
            print("Kontak berhasil ditambahkan")

        elif pilih == 2:
            nama = input("Masukkan nama yang dicari : ")

            hasil = bst.search(nama)

            if hasil:
                print("Kontak ditemukan")
                print(f"Nama   : {hasil.nama}")
                print(f"Nomor  : {hasil.nomor}")
            else:
                print("Kontak tidak ditemukan")

        elif pilih == 3:
            print("\nDaftar Kontak:")
            bst.inorder(bst.root)

        elif pilih == 4:
            print("\nPreorder:")
            bst.preorder(bst.root)

        elif pilih == 5:
            print("\nPostorder:")
            bst.postorder(bst.root)

        elif pilih == 6:
            awal = bst.find_first_contact(bst.root)

            if awal:
                print(f"Kontak pertama : {awal.nama} - {awal.nomor}")
            else:
                print("Daftar kontak kosong")

        elif pilih == 7:
            print(f"Jumlah kontak : {bst.count_contacts(bst.root)}")

        elif pilih == 8:
            print("Program selesai.")

        else:
            print("Pilihan tidak valid!")

if __name__ == "__main__":
    main()
