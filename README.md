# Neovim + LazyVim Cheat Sheet In Indonesian

Keymap di sini mengikuti default LazyVim (picker dan explorer pakai Snacks). Kalau ada yang tidak jalan, cek `Space sk` atau `:verbose map <key>`. Keymap yang ditandai (extra) cuma aktif kalau extra-nya dinyalakan lewat `:LazyExtras`.

## Notasi

- `Space` = `<leader>`, `\` = `<localleader>`
- `C-x` = Ctrl+x, `A-x` = Alt+x, `S-x` = Shift+x
- `Space sg` artinya tekan Space, lalu `s`, lalu `g` berurutan
- `{char}` = satu karakter bebas, `{motion}` = gerakan apa saja, `N` = angka
- Semua tabel berlaku di Normal mode kecuali disebutkan lain
- Bingung lagi di mode apa: tekan `Esc`

Tekan `Space` lalu tunggu sebentar, which-key akan menampilkan semua lanjutan keymap yang tersedia. Ini cara tercepat buat belajar.

## Mode

|Mode|Fungsi|Masuk|Keluar|
|---|---|---|---|
|Normal|Navigasi dan perintah|`Esc`|-|
|Insert|Mengetik|`i` `a` `o` dst|`Esc`|
|Visual|Memilih teks|`v` `V` `C-v`|`Esc`|
|Command|Menjalankan `:command`|`:`|`Esc`|
|Replace|Menimpa teks|`R`|`Esc`|
|Terminal|Mengetik ke shell|`Space ft`|`C-\` lalu `C-n`|

### Masuk Insert mode

| Key       | Fungsi                                                                                      |
| --------- | ------------------------------------------------------------------------------------------- |
| `i` / `a` | Sebelum / sesudah kursor                                                                    |
| `I` / `A` | Awal teks baris / akhir baris                                                               |
| `o` / `O` | Baris baru di bawah / di atas                                                               |
| `C`       | Hapus sampai akhir baris, lalu insert                                                       |
| `S`       | Hapus isi baris, lalu insert (di LazyVim `S` dipakai flash, lihat bagian Flash; pakai `cc`) |
| `gi`      | Insert di posisi terakhir kali insert                                                       |

Di Insert mode:

|Key|Fungsi|
|---|---|
|`C-w`|Hapus satu kata ke belakang|
|`C-u`|Hapus sampai awal baris|
|`C-o`|Jalankan satu perintah Normal mode lalu balik ke Insert|
|`C-r {reg}`|Tempel isi register, misal `C-r 0` atau `C-r +`|
|`A-j` / `A-k`|Pindahkan baris ke bawah / atas|
|`C-s`|Simpan|

## Simpan dan keluar

|Key / Command|Fungsi|
|---|---|
|`C-s`|Simpan (Normal, Insert, Visual)|
|`:w`|Simpan|
|`:wa`|Simpan semua|
|`:q`|Tutup window|
|`:wq` / `:x`|Simpan lalu tutup|
|`:qa`|Tutup semua|
|`:q!`|Tutup tanpa simpan|
|`:qa!`|Tutup semua tanpa simpan|
|`Space qq`|Keluar dari semua|
|`Space qs`|Restore session folder ini|
|`Space ql`|Restore session terakhir|
|`:e!`|Buang perubahan, muat ulang file dari disk|

`Space w` bukan simpan. Itu prefix untuk perintah window (sama seperti `C-w`).

## Gerakan

### Dalam baris dan layar

|Key|Fungsi|
|---|---|
|`h j k l`|Kiri, bawah, atas, kanan|
|`0`|Kolom pertama|
|`^`|Karakter pertama non-spasi|
|`$`|Akhir baris|
|`g_`|Karakter terakhir non-spasi|
|`+` / `-`|Awal baris berikutnya / sebelumnya|
|`H` / `M` / `L`|Atas / tengah / bawah layar|
|`C-d` / `C-u`|Setengah layar turun / naik|
|`C-f` / `C-b`|Satu layar turun / naik|
|`C-e` / `C-y`|Scroll satu baris turun / naik|
|`zz` / `zt` / `zb`|Kursor ke tengah / atas / bawah layar|

### Kata, baris, dan blok

|Key|Fungsi|
|---|---|
|`w` / `b`|Awal kata berikutnya / sebelumnya|
|`e` / `ge`|Akhir kata berikutnya / sebelumnya|
|`W` `B` `E`|Sama, tapi pemisahnya hanya spasi (WORD)|
|`gg` / `G`|Baris pertama / terakhir|
|`Ngg` atau `:N`|Ke baris N|
|`%`|Lompat ke pasangan `()` `[]` `{}`|
|`{` / `}`|Paragraf sebelumnya / berikutnya|
|`f{char}` / `F{char}`|Ke karakter berikutnya / sebelumnya di baris|
|`t{char}` / `T{char}`|Sama, berhenti satu karakter sebelumnya|
|`;` / `,`|Ulangi / balik arah f, F, t, T|
|`C-g`|Info file dan posisi kursor|

Count bisa digabung dengan hampir semua gerakan dan operator:

```text
5j       turun 5 baris
3w       maju 3 kata
2dd      hapus 2 baris
3>>      indent 3 baris
```

### Flash (lompat cepat)

LazyVim memakai flash.nvim, jadi `s` dan `S` tidak lagi bekerja seperti bawaan Vim.

|Key|Fungsi|
|---|---|
|`s{char}{char}`|Lompat ke tempat yang cocok, pilih label yang muncul|
|`S`|Pilih node treesitter (fungsi, blok, argumen)|
|`r`|Remote flash, dipakai setelah operator. Contoh `yr...` salin teks di tempat lain tanpa pindah kursor|
|`R`|Treesitter search (Operator / Visual)|
|`C-s`|Aktif/matikan flash saat mengetik pencarian `/`|
|`C-Space`|Perluas seleksi treesitter. Tekan lagi untuk memperluas, `Backspace` untuk menyusutkan|

## Edit

Pola dasarnya: operator + gerakan, atau operator + text object.

|Operator|Fungsi|
|---|---|
|`d`|Hapus|
|`c`|Ganti (hapus lalu insert)|
|`y`|Salin (yank)|
|`>` / `<`|Indent kanan / kiri|
|`=`|Auto-indent|
|`gq`|Rapikan / wrap teks|
|`gu` / `gU` / `g~`|Lowercase / uppercase / toggle case|
|`gc`|Comment / uncomment|

Menggandakan operator berarti satu baris penuh: `dd`, `yy`, `cc`, `>>`, `gcc`, `guu`, `gUU`.

### Text object

`i` = isi saja, `a` = isi beserta pembungkusnya.

|Object|Arti|
|---|---|
|`w`|Kata|
|`s` / `p`|Kalimat / paragraf|
|`(` `)` `b`|Dalam tanda kurung|
|`[` `]`|Kurung siku|
|`{` `}` `B`|Kurung kurawal|
|`<` `>`|Angle bracket|
|`"` `'` `` ` ``|String|
|`t`|Tag HTML|

LazyVim menambah beberapa lewat mini.ai dan treesitter:

|Object|Arti|
|---|---|
|`f`|Fungsi|
|`c`|Class|
|`a`|Argumen / parameter|
|`o`|Blok, kondisi, atau loop|
|`u`|Pemanggilan fungsi|
|`q`|Kutip apa saja (`"` `'` `` ` ``)|
|`e`|Satu kata camelCase / snake_case|
|`g`|Seluruh buffer|

Awalan `n` dan `l` mencari objek berikutnya / terakhir, misal `cin(` mengganti isi kurung berikutnya.

```text
ciw      ganti satu kata
ci"      ganti isi string
dap      hapus satu paragraf beserta baris kosongnya
yif      salin isi fungsi
daa      hapus satu argumen (beserta komanya)
vaf      pilih seluruh fungsi
gUiw     uppercase satu kata
```

### Hapus, salin, tempel

|Key|Fungsi|
|---|---|
|`x` / `X`|Hapus karakter di / sebelum kursor|
|`dd`|Hapus baris|
|`D`|Hapus sampai akhir baris|
|`yy` / `Y`|Salin baris|
|`p` / `P`|Tempel setelah / sebelum kursor|
|`gp` / `gP`|Tempel, kursor pindah ke akhir teks tempelan|
|`J`|Gabung baris dengan baris di bawah|
|`gJ`|Gabung tanpa menambah spasi|
|`xp`|Tukar dua karakter|
|`ddp`|Tukar baris dengan baris di bawahnya|
|`A-j` / `A-k`|Pindahkan baris atau seleksi ke bawah / atas|
|`C-a` / `C-x`|Tambah / kurangi angka di bawah kursor (`5C-a` tambah 5)|

### Undo, redo, ulang

|Key|Fungsi|
|---|---|
|`u`|Undo|
|`C-r`|Redo|
|`U`|Undo semua perubahan di baris terakhir yang diubah|
|`.`|Ulangi perubahan terakhir|
|`&`|Ulangi substitusi terakhir di baris ini|
|`@:`|Ulangi command `:` terakhir|
|`Space su`|Undo tree (lihat riwayat perubahan)|

### Clipboard dan register

LazyVim mengatur `clipboard=unnamedplus` (kecuali di sesi SSH), jadi `y` dan `p` biasa sudah memakai clipboard sistem. Di Linux butuh provider seperti `wl-clipboard` (Wayland) atau `xclip` / `xsel` (X11). Cek dengan `:checkhealth provider`.

|Key|Fungsi|
|---|---|
|`"ayy`|Salin baris ke register `a`|
|`"ap`|Tempel dari register `a`|
|`"_dd`|Hapus tanpa menimpa register (black hole)|
|`"0p`|Tempel yank terakhir (tidak tertimpa oleh `d`)|
|`"+p`|Tempel dari clipboard sistem secara eksplisit|
|`".`|Teks terakhir yang diketik di Insert mode|
|`"%`|Nama file saat ini|
|`:registers` atau `Space s"`|Lihat semua register|

Kalau kamu paste di atas seleksi (`vp`), teks yang tertimpa masuk ke register. Pakai `"_d` dulu kalau tidak mau yank-mu hilang.

## Visual mode

|Key|Fungsi|
|---|---|
|`v` / `V` / `C-v`|Karakter / baris / blok|
|`gv`|Pilih ulang seleksi terakhir|
|`o`|Pindah ke ujung seleksi satunya|
|`d` `c` `y` `p`|Hapus, ganti, salin, tempel menimpa seleksi|
|`>` / `<`|Indent (seleksi tetap aktif di LazyVim)|
|`A-j` / `A-k`|Pindahkan seleksi ke bawah / atas|
|`U` / `u` / `~`|Uppercase / lowercase / toggle|
|`gc`|Comment / uncomment seleksi|
|`:`|Command dengan range `'<,'>` otomatis|
|`g C-a`|Tambah angka bertingkat di seleksi baris (1, 2, 3, ...)|

Visual block (`C-v`) untuk edit banyak baris sekaligus:

```text
C-v  j j j    pilih kolom di 4 baris
I  teks  Esc  sisipkan teks di awal semua baris
A  teks  Esc  tambahkan teks di akhir blok
$A  teks  Esc tambahkan di akhir tiap baris (panjang baris berbeda)
c  teks  Esc  ganti isi blok
```

## Cari dan ganti

### Dalam file

|Key|Fungsi|
|---|---|
|`/pattern` / `?pattern`|Cari ke bawah / ke atas|
|`n` / `N`|Hasil berikutnya / sebelumnya|
|`*` / `#`|Cari kata di bawah kursor ke bawah / ke atas|
|`Esc`|Hilangkan highlight pencarian|
|`Space sb`|Cari baris di buffer ini lewat picker|

### Ganti (substitute)

```vim
:[range]s/lama/baru/[flag]
```

|Command|Fungsi|
|---|---|
|`:s/a/b/`|Ganti yang pertama di baris ini|
|`:s/a/b/g`|Ganti semua di baris ini|
|`:%s/a/b/g`|Ganti di seluruh file|
|`:%s/a/b/gc`|Dengan konfirmasi satu per satu|
|`:'<,'>s/a/b/g`|Hanya di seleksi|
|`:%s//b/g`|Pola kosong = pakai pencarian terakhir|
|`:%s/\<kata\>/baru/g`|Cocokkan kata utuh|

Flag `c` menampilkan konfirmasi: `y` ganti, `n` lewati, `a` ganti semua sisanya, `q` berhenti.

Cara yang sering lebih cepat dari `:s`: `cgn`.

```text
*          cari kata di bawah kursor
cgn        ganti kecocokan berikutnya, ketik teks baru, Esc
.          ulangi untuk kecocokan berikutnya (n untuk lewati)
```

### Seluruh project

|Key|Fungsi|
|---|---|
|`Space /` atau `Space sg`|Grep di root project|
|`Space sG`|Grep di cwd|
|`Space sw`|Grep kata di bawah kursor / seleksi|
|`Space sr`|Cari dan ganti di project (grug-far)|
|`Space sR`|Buka lagi picker terakhir|

Alur umum untuk rename teks di banyak file: `Space sr`, isi pola dan pengganti, lihat preview hasilnya, lalu jalankan replace.

## Command Ex yang sering dipakai

|Command|Fungsi|
|---|---|
|`:g/pola/d`|Hapus semua baris yang cocok|
|`:v/pola/d`|Hapus semua baris yang tidak cocok|
|`:g/pola/normal A;`|Jalankan perintah Normal mode di tiap baris yang cocok|
|`:normal @a`|Jalankan macro di baris tertentu (dengan range)|
|`:sort` / `:sort u`|Urutkan baris / urutkan dan buang duplikat|
|`:r file`|Sisipkan isi file|
|`:r !perintah`|Sisipkan output command shell|
|`:%!perintah`|Lewatkan seluruh buffer ke command shell, ganti dengan hasilnya|
|`:%y`|Salin seluruh file|
|`:noh`|Hapus highlight pencarian|
|`:set wrap!`|Toggle opsi (tanda `!` membalik nilai)|
|`:Inspect`|Info highlight group dan treesitter di bawah kursor|
|`q:`|Buka riwayat command sebagai buffer yang bisa diedit|

## Marks dan riwayat posisi

|Key|Fungsi|
|---|---|
|`ma`|Buat mark lokal `a`|
|`` `a ``|Ke posisi persis mark `a`|
|`'a`|Ke baris mark `a`|
|`mA`|Mark global (antar file)|
|``|Kembali ke posisi sebelum lompatan terakhir|
|`` `. ``|Ke posisi perubahan terakhir|
|`C-o` / `C-i`|Mundur / maju di jump list|
|`g;` / `g,`|Ke perubahan sebelumnya / berikutnya|
|`Space sm`|Daftar mark lewat picker|
|`Space sj`|Daftar jump lewat picker|

## Pindah antar bagian kode

|Key|Fungsi|
|---|---|
|`]]` / `[[`|Referensi berikutnya / sebelumnya dari kata di bawah kursor|
|`]f` / `[f`|Awal fungsi berikutnya / sebelumnya|
|`]c` / `[c`|Class berikutnya / sebelumnya|
|`]a` / `[a`|Argumen berikutnya / sebelumnya|
|`]d` / `[d`|Diagnostic berikutnya / sebelumnya|
|`]e` / `[e`|Error berikutnya / sebelumnya|
|`]w` / `[w`|Warning berikutnya / sebelumnya|
|`]h` / `[h`|Hunk git berikutnya / sebelumnya|
|`]t` / `[t`|Komentar TODO berikutnya / sebelumnya|
|`]q` / `[q`|Item quickfix berikutnya / sebelumnya|
|`]b` / `[b`|Buffer berikutnya / sebelumnya|

## Surround dan comment

|Key|Fungsi|
|---|---|
|`gcc`|Comment / uncomment baris|
|`gc{motion}`|Comment hasil gerakan, misal `gcap` untuk satu paragraf|
|`gc` (Visual)|Comment seleksi|
|`gco` / `gcO`|Tambah baris komentar di bawah / di atas|

Surround (mini.surround, extra `coding.mini-surround`):

|Key|Fungsi|
|---|---|
|`gsa{motion}{char}`|Tambah pembungkus. `gsaiw"` bungkus kata dengan `"`|
|`gsd{char}`|Hapus pembungkus. `gsd"`|
|`gsr{lama}{baru}`|Ganti pembungkus. `gsr"'` ubah `"` jadi `'`|
|`gsf` / `gsF`|Cari pembungkus ke kanan / kiri|
|`gsh`|Highlight pembungkus|

## Buffer, window, tab

### Buffer

|Key|Fungsi|
|---|---|
|`Space ,` atau `Space fb`|Pilih buffer lewat picker|
|`S-h` / `S-l`|Buffer sebelumnya / berikutnya|
|`Space bb` atau `` Space ` ``|Balik ke buffer sebelumnya|
|`Space bd`|Tutup buffer|
|`Space bo`|Tutup semua buffer lain|
|`Space bi`|Tutup buffer yang tidak terlihat|
|`Space bD`|Tutup buffer beserta window-nya|
|`Space bp`|Pin buffer|
|`Space bP`|Tutup semua buffer yang tidak di-pin|
|`Space bl` / `Space br`|Tutup buffer di kiri / kanan|
|`Space bj`|Pilih buffer dengan huruf (bufferline)|
|`[B` / `]B`|Geser posisi buffer di bufferline|
|`Space fn`|File baru|
|`:ls`|Daftar buffer|

### Window

|Key|Fungsi|
|---|---|
|`Space \|`|Split ke kanan|
|`Space -`|Split ke bawah|
|`C-h` `C-j` `C-k` `C-l`|Pindah ke window kiri / bawah / atas / kanan|
|`C-Up` `C-Down` `C-Left` `C-Right`|Ubah ukuran window|
|`Space wd`|Tutup window|
|`Space wm`|Zoom window (toggle maximize)|
|`C-w =`|Samakan ukuran semua window|
|`C-w o`|Sisakan window ini saja|
|`C-w x`|Tukar dengan window sebelah|
|`C-w H/J/K/L`|Pindahkan window ke tepi kiri / bawah / atas / kanan|
|`C-w T`|Pindahkan window ke tab baru|
|`Space w` + tombol|Sama dengan `C-w` + tombol|
|`C-w Space`|Mode window (which-key hydra)|

### Tab

|Key|Fungsi|
|---|---|
|`Space Tab Tab`|Tab baru|
|`Space Tab ]` / `[`|Tab berikutnya / sebelumnya|
|`Space Tab d`|Tutup tab|
|`Space Tab o`|Tutup tab lain|
|`Space Tab f` / `l`|Tab pertama / terakhir|

Di LazyVim buffer dan split biasanya lebih sering dipakai daripada tab.

## Picker (Snacks)

### Mencari file dan teks

|Key|Fungsi|
|---|---|
|`Space Space` atau `Space ff`|Cari file di root project|
|`Space fF`|Cari file di cwd|
|`Space fg`|Cari file yang dilacak git|
|`Space fr` / `Space fR`|File terakhir dibuka (global / cwd)|
|`Space fc`|File konfigurasi Neovim|
|`Space fp`|Daftar project|
|`Space /`|Grep di project|
|`Space :` atau `Space sc`|Riwayat command|
|`Space sC`|Daftar semua command|
|`Space sk`|Cari keymap|
|`Space sh`|Cari halaman help|
|`Space ss` / `Space sS`|Simbol LSP (file / workspace)|
|`Space sd` / `Space sD`|Diagnostic (workspace / buffer)|
|`Space st` / `Space sT`|Komentar TODO / hanya TODO, FIX, FIXME|
|`Space sa`|Autocmd|
|`Space sH`|Highlight group|
|`Space uC`|Ganti colorscheme|

### Di dalam picker

|Key|Fungsi|
|---|---|
|`Enter`|Buka|
|`C-s` / `C-v`|Buka di split horizontal / vertikal|
|`Tab`|Tandai item|
|`C-q`|Kirim hasil ke quickfix|
|`A-i`|Toggle file ter-ignore (gitignore)|
|`A-h`|Toggle file tersembunyi|
|`C-j` / `C-k`|Item berikutnya / sebelumnya|
|`C-d` / `C-u`|Scroll daftar|
|`C-f` / `C-b`|Scroll preview|
|`Esc`|Tutup|

Kalau file di `node_modules` atau `vendor` tidak ketemu, itu karena di-ignore. Tekan `A-i` di picker.

Kalau kamu pindah ke Telescope atau fzf-lua lewat extra, binding di dalam picker sedikit berbeda (Telescope: `C-x` split horizontal, `C-t` tab baru).

## File explorer

|Key|Fungsi|
|---|---|
|`Space e`|Toggle explorer (root project)|
|`Space E`|Explorer di cwd|
|`Space fe` / `Space fE`|Sama seperti di atas|

Di dalam explorer Snacks:

|Key|Fungsi|
|---|---|
|`Enter` / `l`|Buka file atau expand folder|
|`h`|Tutup folder|
|`a`|Buat file (akhiri dengan `/` untuk folder)|
|`r`|Rename|
|`d`|Hapus|
|`c` / `m`|Tandai untuk copy / move|
|`p`|Paste hasil copy / move|
|`y`|Salin path|
|`o`|Buka dengan aplikasi sistem|
|`H`|Toggle file tersembunyi|
|`I`|Toggle file ter-ignore|
|`P`|Toggle preview|
|`BS`|Naik satu direktori|
|`?`|Bantuan|

## LSP dan coding

LSP server harus sudah terpasang (`:Mason`) supaya keymap ini bekerja.

|Key|Fungsi|
|---|---|
|`gd`|Ke definisi|
|`gD`|Ke deklarasi|
|`gr`|Daftar referensi|
|`gI`|Ke implementasi|
|`gy`|Ke type definition|
|`K`|Hover (dokumentasi)|
|`gK` atau `C-k` (Insert)|Signature help|
|`Space ca`|Code action|
|`Space cA`|Source action|
|`Space cr`|Rename simbol|
|`Space cR`|Rename file|
|`Space cf`|Format (file atau seleksi)|
|`Space cF`|Format injected language (misal CSS di dalam HTML)|
|`Space co`|Organize imports (tergantung bahasa)|
|`Space cc` / `Space cC`|Jalankan / refresh codelens|
|`Space cd`|Diagnostic di baris ini|
|`Space cl`|Info LSP|
|`Space cs`|Daftar simbol file (Trouble)|
|`Space cS`|Referensi / definisi (Trouble)|
|`gai` / `gao`|Incoming / outgoing calls|
|`Space cm`|Mason|

### Autocomplete (Insert mode)

Default LazyVim memakai blink.cmp.

|Key|Fungsi|
|---|---|
|`Enter`|Terima saran|
|`C-n` / `C-p`|Saran berikutnya / sebelumnya|
|`C-Space`|Buka menu / dokumentasi|
|`C-e`|Tutup menu|
|`Tab` / `S-Tab`|Lompat antar placeholder snippet|

### Diagnostic dan Trouble

|Key|Fungsi|
|---|---|
|`Space xx`|Diagnostic seluruh workspace (Trouble)|
|`Space xX`|Diagnostic buffer ini|
|`Space xq` / `Space xl`|Quickfix / location list|
|`Space xQ` / `Space xL`|Quickfix / location list versi Trouble|
|`Space xt` / `Space xT`|TODO (Trouble)|
|`:copen` / `:cclose`|Buka / tutup quickfix|
|`:cn` / `:cp`|Item quickfix berikutnya / sebelumnya|

### Format otomatis

|Key|Fungsi|
|---|---|
|`Space uf`|Toggle auto-format (global)|
|`Space uF`|Toggle auto-format (buffer ini)|
|`:ConformInfo`|Lihat formatter yang aktif|

## Git

|Key|Fungsi|
|---|---|
|`Space gg`|LazyGit (root project)|
|`Space gG`|LazyGit (cwd)|
|`Space gs`|Git status|
|`Space gd` / `Space gD`|Diff hunk / diff terhadap origin|
|`Space gl` / `Space gL`|Git log (root / cwd)|
|`Space gf`|Riwayat file ini|
|`Space gb`|Blame baris ini|
|`Space gB`|Buka file di GitHub / GitLab di browser|
|`Space gY`|Salin link GitHub / GitLab|
|`Space gS`|Git stash|

Aksi hunk (gitsigns):

|Key|Fungsi|
|---|---|
|`]h` / `[h`|Hunk berikutnya / sebelumnya|
|`Space ghs`|Stage hunk|
|`Space ghr`|Reset hunk|
|`Space ghS`|Stage seluruh buffer|
|`Space ghR`|Reset seluruh buffer|
|`Space ghu`|Undo stage hunk|
|`Space ghp`|Preview hunk|
|`Space ghb`|Blame baris ini|
|`Space ghd`|Diff file ini|
|`ih` (Operator / Visual)|Text object untuk hunk|

Di dalam LazyGit: `?` bantuan, `space` stage / unstage, `c` commit, `P` push, `p` pull, `q` keluar.

## Terminal

|Key|Fungsi|
|---|---|
|`Space ft`|Terminal di root project|
|`Space fT`|Terminal di cwd|
|`C-/`|Toggle terminal (juga untuk menyembunyikannya dari dalam terminal)|
|`C-\` lalu `C-n`|Keluar dari Terminal mode ke Normal mode|
|`:terminal`|Terminal di window biasa|

Di Terminal mode hampir semua tombol dikirim ke shell, jadi balik ke Normal mode dulu sebelum pindah window.

## Folding

|Key|Fungsi|
|---|---|
|`za`|Toggle fold|
|`zo` / `zc`|Buka / tutup fold|
|`zO` / `zC`|Buka / tutup rekursif|
|`zR` / `zM`|Buka semua / tutup semua|
|`zv`|Buka fold sampai kursor terlihat|
|`zj` / `zk`|Awal fold berikutnya / akhir fold sebelumnya|
|`zf{motion}`|Buat fold manual|
|`zd`|Hapus fold manual|

## Macro

```text
qa          mulai rekam ke register a
...         lakukan perubahan
q           berhenti
@a          jalankan
@@          ulangi macro terakhir
10@a        jalankan 10 kali
```

Tips: akhiri rekaman dengan gerakan ke baris berikutnya (`j` atau `0j`), supaya `10@a` otomatis berlanjut ke baris-baris di bawahnya. Untuk menjalankan macro di banyak baris sekaligus, pilih baris dengan `V` lalu `:normal @a`.

## Toggle UI

|Key|Fungsi|
|---|---|
|`Space uw`|Word wrap|
|`Space ul`|Nomor baris|
|`Space uL`|Nomor relatif|
|`Space us`|Spell check|
|`Space ud`|Diagnostic|
|`Space uh`|Inlay hints|
|`Space ug`|Indent guides|
|`Space uT`|Treesitter highlight|
|`Space ub`|Latar gelap / terang|
|`Space uz`|Zen mode|
|`Space uZ`|Zoom mode|
|`Space ui` / `Space uI`|Inspect posisi / tree treesitter|
|`Space un`|Tutup semua notifikasi|
|`Space n`|Riwayat notifikasi|
|`Space snl` / `Space snh`|Pesan terakhir / riwayat pesan (noice)|
|`Space .`|Scratch buffer|
|`Space S`|Pilih scratch buffer|

## Plugin dan tool

|Command / Key|Fungsi|
|---|---|
|`Space l` atau `:Lazy`|Plugin manager|
|`Space L`|Changelog LazyVim|
|`:LazyExtras`|Aktif / nonaktifkan extras|
|`Space cm` atau `:Mason`|Install LSP, formatter, linter|
|`:Lazy sync`|Install, update, dan bersihkan sekaligus|
|`:checkhealth`|Cek kesehatan Neovim dan plugin|
|`:checkhealth vim.lsp`|Cek LSP (pengganti `:LspInfo` di Neovim 0.11+)|
|`:LspRestart`|Restart LSP server|
|`Space sp`|Cari plugin spec|

Di dalam jendela `:Lazy`: `I` install, `U` update, `S` sync, `X` clean, `L` log, `P` profile, `?` bantuan. Di dalam `:Mason`: `i` install, `X` hapus, `U` update semua, `g?` bantuan.

Konfigurasi pribadi ada di `~/.config/nvim/lua/`:

```text
config/options.lua     opsi (vim.opt)
config/keymaps.lua     keymap tambahan
config/autocmds.lua    autocmd
plugins/*.lua          plugin tambahan atau override
```

## Troubleshooting

Lupa shortcut:

1. `Space sk`, ketik nama aksi (`format`, `terminal`, `definition`)
2. Atau tekan `Space` lalu tunggu, lihat menu which-key
3. `Space ?` untuk keymap khusus buffer ini
4. `:verbose nmap <key>` untuk tahu siapa yang mendefinisikan

Shortcut tidak jalan:

- Pastikan di mode yang benar, tekan `Esc` lalu coba lagi
- Plugin atau extra-nya mungkin belum aktif: cek `:Lazy` dan `:LazyExtras`
- Untuk keymap LSP, cek server aktif: `Space cl`
- Terminal emulator bisa menangkap tombol tertentu (`C-/`, `C-Space`, `A-j`). Coba di terminal lain atau cek binding emulatornya
- Pesan error ada di `:messages`

Clipboard tidak nyambung:

- `:checkhealth provider`, pastikan `wl-clipboard` atau `xclip` terpasang
- Di sesi SSH LazyVim sengaja tidak memakai clipboard sistem

Cek mapping:

```vim
:verbose nmap <leader>ff
:verbose nmap gd
:verbose imap <C-k>
```

## Alur kerja harian

Buka project dan mulai kerja:

```bash
cd ~/project
nvim
```

```text
Space Space       cari file
Space /           cari teks di project
gd                ke definisi
K                 lihat dokumentasi
Space ca          code action
C-s               simpan
Space gg          LazyGit
```

Edit satu fungsi:

```text
Space /           cari nama fungsi, Enter
vif               pilih isi fungsi
Space cr          rename simbol
Space cf          format
]d                lompat ke diagnostic berikutnya
```

Salin kode antar file:

```text
V  j j            pilih baris
y                 salin
Space Space       buka file tujuan
p                 tempel
Space cf          format
```

Ganti kata di seluruh file:

```text
*                 cari kata di bawah kursor
cgn  baru  Esc    ganti yang pertama
.  .  .           ulangi (atau n untuk melewati)
```

## Urutan belajar

Level 1, dasar:

```text
Esc  i a o
C-s  :q
h j k l   w b   0 $   gg G
u  C-r
dd yy p
Space Space   Space /   Space sk
```

Level 2, produktif:

```text
v V   ciw diw yiw   ci" ci(
f t ;   s (flash)
cgn  .
Space e   S-h S-l   C-h/j/k/l
gd K gr   Space ca  Space cr  Space cf
gcc  gsa
```

Level 3, lanjutan:

```text
macro   register   marks
:g  :normal  :sort
text object lanjutan (af, ia, ao)
quickfix  Trouble
LazyGit  gitsigns hunk
grug-far (Space sr)
keymap sendiri di config/keymaps.lua
```

## Referensi satu layar

```text
MODE
Esc                 Normal
i a o               Insert
v V C-v             Visual
:                   Command

SIMPAN / KELUAR
C-s                 simpan
:q  :wq  :qa!       keluar
Space qq            keluar semua

GERAK
h j k l             kiri bawah atas kanan
w b e               per kata
0 ^ $               awal / isi pertama / akhir baris
gg G                awal / akhir file
C-d C-u             setengah layar
f{c} t{c}           ke karakter di baris
s{c}{c}             flash
%                   pasangan kurung

EDIT
dd yy p P           hapus salin tempel
u C-r .             undo redo ulang
ciw diw yiw         kata
ci" ci( cif         isi string / kurung / fungsi
gcc                 comment
A-j A-k             pindah baris
cgn                 ganti kecocokan, ulang dengan .

CARI
/pat  n  N          cari dalam file
* #                 kata di bawah kursor
Space /             grep project
Space sr            cari dan ganti project

FILE / BUFFER / WINDOW
Space Space         cari file
Space ,             buffer
Space e             explorer
S-h S-l             buffer prev / next
Space bd            tutup buffer
Space | / Space -   split kanan / bawah
C-h/j/k/l           pindah window
Space wd            tutup window

LSP / KODE
gd gr gI            definisi referensi implementasi
K                   hover
Space ca            code action
Space cr            rename
Space cf            format
Space cd            diagnostic baris
]d [d               diagnostic next / prev
Space xx            daftar diagnostic

GIT / LAIN
Space gg            LazyGit
]h [h               hunk next / prev
Space ghs ghr ghp   stage reset preview hunk
Space ft            terminal
Space sk            cari keymap
Space l             Lazy
Space cm            Mason
```
