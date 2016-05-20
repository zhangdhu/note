    
    /**
     * 写文件
     * 
     * @param path
     *            文件的路径
     * @param content
     *            写入文件的内容
     */
    public static void writerText(String path, String content) {
        File dirFile = new File(path);
        if (!dirFile.exists()) {
            dirFile.mkdir();
        }
        try {
            //new FileWriter(path + "t.txt", true)  这里加入true 可以不覆盖原有TXT文件内容 续写
            BufferedWriter bw1 = new BufferedWriter(new FileWriter(path + "t.txt", true));
            bw1.write(content);
            bw1.flush();
            bw1.close();
        } catch (IOException e) {
            e.printStackTrace();
        }