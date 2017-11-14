public function exportUnlearnList()
{
    $unlearnList = $this->getUnlearnList();
    $date = date('Ymd');
    $filename = 'ibl_unlearn_'.$date;
    $reportData = $unlearnList;
    $reportHeader = ['用户名', '学生', '班级ID', '班级名', '学校名', '区域', '主教', '上课次数', '截止有效期', '班主任', '年级组'];
    Excel::create($filename, function($excel) use($reportData, $reportHeader){
        $excel->sheet('Sheetname', function($sheet) use($reportData, $reportHeader) {

            $sheet->fromArray($reportData);

            $cells = range('A', 'Z');
            foreach ($reportHeader as $k=>$item) {
                $sheet->cell($cells[$k] . '1', function ($cell) use ($k, $reportHeader) {
                    // manipulate the cell
                    $cell->setValue($reportHeader[$k]);
                    if ($k == 0) {
                        $cell->setBackground('#000000');
                    }
                });
            }
        });

    })->download('csv');

}
