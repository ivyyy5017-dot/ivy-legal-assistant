{
  "name": "ivy-legal-assistant",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint .",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^19.2.0",
    "react-dom": "^19.2.0",
    "react-router-dom": "^7.1.1",
    "lucide-react": "^0.474.0",
    "@radix-ui/react-slot": "^1.1.1",
    "@radix-ui/react-dialog": "^1.1.4",
    "@radix-ui/react-dropdown-menu": "^2.1.4",
    "@radix-ui/react-tabs": "^1.1.2",
    "@radix-ui/react-toast": "^1.2.4",
    "@radix-ui/react-select": "^2.1.4",
    "@radix-ui/react-label": "^2.1.1",
    "class-variance-authority": "^0.7.1",
    "clsx": "^2.1.1",
    "tailwind-merge": "^2.6.0"
  },
  "devDependencies": {
    "@eslint/js": "^9.39.1",
    "@types/node": "^22.10.2",
    "@types/react": "^19.2.0",
    "@types/react-dom": "^19.2.0",
    "@vitejs/plugin-react": "^4.3.4",
    "autoprefixer": "^10.4.20",
    "eslint": "^9.39.1",
    "eslint-plugin-react-hooks": "^5.0.0",
    "eslint-plugin-react-refresh": "^0.4.16",
    "globals": "^15.14.0",
    "postcss": "^8.4.49",
    "tailwindcss": "^3.4.17",
    "typescript": "~5.6.3",
    "typescript-eslint": "^8.20.0",
    "vite": "^6.0.7"
  }
import { BrowserRouter, Routes, Route } from 'react-router-dom'
import { MainLayout } from '@/components/layout/MainLayout'
import Dashboard from '@/pages/Dashboard'
import Cases from '@/pages/Cases'
import Templates from '@/pages/Templates'
import Regulations from '@/pages/Regulations'
import DocumentGenerate from '@/pages/DocumentGenerate'
import SettingsPage from '@/pages/Settings'

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<MainLayout />}>
          <Route index element={<Dashboard />} />
          <Route path="cases" element={<Cases />} />
          <Route path="templates" element={<Templates />} />
          <Route path="regulations" element={<Regulations />} />
          <Route path="generate" element={<DocumentGenerate />} />
          <Route path="settings" element={<SettingsPage />} />
          <Route path="help" element={<div className="p-8 text-center text-legal-500">帮助中心 - 即将上线</div>} />
        </Route>
      </Routes>
    </BrowserRouter>
  )
}

export default App
import React from 'react'
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/components/ui/card'
import { Button } from '@/components/ui/button'
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs'
import {
  FolderOpen,
  FileText,
  Scale,
  Clock,
  CheckCircle,
  AlertCircle,
  ArrowRight,
  Plus,
  Upload
} from 'lucide-react'

const recentCases = [
  { id: '1', name: '民间借贷纠纷案', status: 'processing', updatedAt: '2小时前' },
  { id: '2', name: '房屋租赁合同争议', status: 'completed', updatedAt: '昨天' },
  { id: '3', name: '离婚纠纷案', status: 'draft', updatedAt: '3天前' },
]

const recentDocuments = [
  { id: '1', name: '民事起诉状_张三诉李四', template: '民事起诉状', createdAt: '1小时前' },
  { id: '2', name: '律师函_催款函', template: '律师函', createdAt: '昨天' },
]

const stats = [
  { label: '进行中案件', value: 12, icon: FolderOpen, color: 'text-blue-600', bg: 'bg-blue-100' },
  { label: '本月生成文书', value: 28, icon: FileText, color: 'text-green-600', bg: 'bg-green-100' },
  { label: '待审核', value: 5, icon: Clock, color: 'text-orange-600', bg: 'bg-orange-100' },
  { label: '已完成', value: 156, icon: CheckCircle, color: 'text-purple-600', bg: 'bg-purple-100' },
]

export default function Dashboard() {
  return (
    <div className="space-y-6 animate-fadeIn">
      <div className="flex items-center justify-between">
        <div>
          <h1 className="text-2xl font-bold text-legal-900">欢迎回来，Ivy</h1>
          <p className="text-legal-500 mt-1">今天是2026年2月27日，您有12个进行中的案件</p>
        </div>
        <div className="flex gap-3">
          <Button variant="outline" className="gap-2">
            <Upload className="w-4 h-4" />
            上传材料
          </Button>
          <Button className="gap-2 bg-legal-800 hover:bg-legal-700">
            <Plus className="w-4 h-4" />
            新建案件
          </Button>
        </div>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
        {stats.map((stat, index) => (
          <Card key={index} className="card-hover">
            <CardContent className="p-6">
              <div className="flex items-center justify-between">
                <div>
                  <p className="text-sm text-legal-500">{stat.label}</p>
                  <p className="text-3xl font-bold text-legal-900 mt-1">{stat.value}</p>
                </div>
                <div className={`w-12 h-12 rounded-lg ${stat.bg} flex items-center justify-center`}>
                  <stat.icon className={`w-6 h-6 ${stat.color}`} />
                </div>
              </div>
            </CardContent>
          </Card>
        ))}
      </div>

      <Tabs defaultValue="cases" className="space-y-4">
        <TabsList>
          <TabsTrigger value="cases">最近案件</TabsTrigger>
          <TabsTrigger value="documents">最近文书</TabsTrigger>
          <TabsTrigger value="tasks">待办事项</TabsTrigger>
        </TabsList>

        <TabsContent value="cases" className="space-y-4">
          <Card>
            <CardHeader className="flex flex-row items-center justify-between">
              <div>
                <CardTitle>进行中的案件</CardTitle>
                <CardDescription>您正在处理的案件列表</CardDescription>
              </div>
              <Button variant="ghost" size="sm" className="gap-1">
                查看全部 <ArrowRight className="w-4 h-4" />
              </Button>
            </CardHeader>
            <CardContent>
              <div className="space-y-4">
                {recentCases.map((caseItem) => (
                  <div key={caseItem.id} className="flex items-center justify-between p-4 rounded-lg border border-legal-200 hover:border-legal-300 hover:bg-legal-50 transition-colors cursor-pointer">
                    <div className="flex items-center gap-4">
                      <div className={`w-10 h-10 rounded-lg flex items-center justify-center ${
                        caseItem.status === 'processing' ? 'bg-blue-100' :
                        caseItem.status === 'completed' ? 'bg-green-100' : 'bg-gray-100'
                      }`}>
                        <Scale className={`w-5 h-5 ${
                          caseItem.status === 'processing' ? 'text-blue-600' :
                          caseItem.status === 'completed' ? 'text-green-600' : 'text-gray-600'
                        }`} />
                      </div>
                      <div>
                        <p className="font-medium text-legal-900">{caseItem.name}</p>
                        <p className="text-sm text-legal-500">更新于 {caseItem.updatedAt}</p>
                      </div>
                    </div>
                    <div className="flex items-center gap-2">
                      <span className={`px-3 py-1 rounded-full text-xs font-medium ${
                        caseItem.status === 'processing' ? 'bg-blue-100 text-blue-700' :
                        caseItem.status === 'completed' ? 'bg-green-100 text-green-700' : 'bg-gray-100 text-gray-700'
                      }`}>
                        {caseItem.status === 'processing' ? '处理中' :
                         caseItem.status === 'completed' ? '已完成' : '草稿'}
                      </span>
                      <ArrowRight className="w-4 h-4 text-legal-400" />
                    </div>
                  </div>
                ))}
              </div>
            </CardContent>
          </Card>
        </TabsContent>

        <TabsContent value="documents" className="space-y-4">
          <Card>
            <CardHeader className="flex flex-row items-center justify-between">
              <div>
                <CardTitle>最近生成的文书</CardTitle>
                <CardDescription>最近创建的法律文书</CardDescription>
              </div>
              <Button variant="ghost" size="sm" className="gap-1">
                查看全部 <ArrowRight className="w-4 h-4" />
              </Button>
            </CardHeader>
            <CardContent>
              <div className="space-y-4">
                {recentDocuments.map((doc) => (
                  <div key={doc.id} className="flex items-center justify-between p-4 rounded-lg border border-legal-200 hover:border-legal-300 hover:bg-legal-50 transition-colors cursor-pointer">
                    <div className="flex items-center gap-4">
                      <div className="w-10 h-10 rounded-lg bg-purple-100 flex items-center justify-center">
                        <FileText className="w-5 h-5 text-purple-600" />
                      </div>
                      <div>
                        <p className="font-medium text-legal-900">{doc.name}</p>
                        <p className="text-sm text-legal-500">{doc.template} · {doc.createdAt}</p>
                      </div>
                    </div>
                    <Button variant="ghost" size="sm">
                      <ArrowRight className="w-4 h-4 text-legal-400" />
                    </Button>
                  </div>
                ))}
              </div>
            </CardContent>
          </Card>
        </TabsContent>

        <TabsContent value="tasks" className="space-y-4">
          <Card>
            <CardHeader>
              <CardTitle>待办事项</CardTitle>
              <CardDescription>需要您处理的任务</CardDescription>
            </CardHeader>
            <CardContent>
              <div className="space-y-4">
                <div className="flex items-start gap-4 p-4 rounded-lg border border-orange-200 bg-orange-50">
                  <AlertCircle className="w-5 h-5 text-orange-600 mt-0.5" />
                  <div className="flex-1">
                    <p className="font-medium text-legal-900">待审核：民间借贷纠纷案文书</p>
                    <p className="text-sm text-legal-500 mt-1">需要检查AI生成的起诉状内容</p>
                  </div>
                  <Button size="sm" variant="outline">处理</Button>
                </div>
                <div className="flex items-start gap-4 p-4 rounded-lg border border-legal-200">
                  <Clock className="w-5 h-5 text-legal-500 mt-0.5" />
                  <div className="flex-1">
                    <p className="font-medium text-legal-900">补充材料：房屋租赁合同争议</p>
                    <p className="text-sm text-legal-500 mt-1">缺少关键证据文件</p>
                  </div>
                  <Button size="sm" variant="ghost">查看</Button>
                </div>
              </div>
            </CardContent>
          </Card>
        </TabsContent>
      </Tabs>
    </div>
  )
}
