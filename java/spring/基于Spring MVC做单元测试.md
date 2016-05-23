#基于Spring MVC做单元测试

package com.zhangdh.quartz.controller;

import com.zhangdh.quartz.model.AppInfo;
import com.zhangdh.quartz.service.AppInfoService;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
import org.springframework.test.context.web.WebAppConfiguration;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;
import org.springframework.web.context.WebApplicationContext;

import static org.mockito.Mockito.verify;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultHandlers.print;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
import static org.hamcrest.CoreMatchers.is;
import java.util.ArrayList;

import static org.mockito.Mockito.when;
@RunWith(SpringJUnit4ClassRunner.class)
@WebAppConfiguration
@ContextConfiguration("file:src/main/configs/spring/mvc-dispatcher-servlet.xml")
public class AppInfoControllerTests {
    private MockMvc mockMvc;

    @Mock
    private AppInfoService appInfoService;

    @InjectMocks
    private AppInfoController appInfoController;


    @Before
    public void setup() {
        MockitoAnnotations.initMocks(this);
        this.mockMvc = MockMvcBuilders.standaloneSetup(appInfoController).build();
    }

    @Test
    public void simple() throws Exception {
        when(appInfoService.findAll(new AppInfo())).thenReturn(new ArrayList<AppInfo>());
        mockMvc.perform(get("/api/app/list")).andDo(print()).andExpect(status().isOk()).andExpect(content().string(is("ok")));
        verify(appInfoService).findAll(new AppInfo());
    }
}
